## Exporting your dialog skill from Watson Assistant

Watson Assistant's user interface includes an "Export Skill" option for easily extracting the JSON version of a Watson Assistant skill.  However, this default format is not optimal for storing in Git for the following reasons:
* The JSON file is one (very long) line
* The JSON file is not organized for easy comparison between versions.

Instead, we use the [Get Workspace API](https://cloud.ibm.com/apidocs/assistant/assistant-v1#getworkspace) to export the skill.

The generalized version of the command is:
```
curl -u "apikey:{apikey}" "{url}/v1/workspaces/{workspace_id}?version={version}&export=true&sort=stable"
```

This command can be augmented with python's `json.tool` which formats the JSON file into a "pretty-printed" line. Below is the generalized syntax I used to export my updates. You'll need to fill in your own `{apikey}` and `{workspace_id}`.  These values can be found by clicking on the "View API Details" option on the skill, from the Watson Assistant Skills page.

```
curl -u "apikey:{apikey}" "https://gateway-wdc.watsonplatform.net/assistant/api/v1/workspaces/{workspace_id}/?export=true&sort=stable&version=2021-03-30" | python -m json.tool > skill-Customer-Service-Skill-Ch2.json
```

The `export=true` option includes all the key details for the skill.  The `sort=stable` option ensures that the skill data is exported in a predictable order, required for easy comparisons.  The `python -m json.tool` "pretty-prints" the JSON into multiple lines.

In the first few commits to Git, I forgot to use this syntax.  Hence, I created a commit "Reset history with comparable export" which reset the history.  All of the commits after that commit are easily compared with each other.
