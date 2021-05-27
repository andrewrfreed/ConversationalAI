# Setup and Troubleshooting
The notebook was built and tested with the version of Jupyter built into my Python 3.7.4 installation.  It should work on other environments but may require a tweak for JupyterLab (see below)

## Code dependencies
The `requirements.txt` file lists the **exact** library versions I tested the notebook on with `==`.  In theory you should be able to use more recent versions of the dependent libraries.  I am reluctant to use the `>=` operator on the dependency versions due to personal experiences fragile backwards compatibility in some Python libraries I have used.

Using different versions is **not guaranteed to work**.  Several of the dependent libraries make breaking API changes in minor releases.  If you already have a version of `pandas` or `scikit-learn` installed you may prefer to setup a separate [Python virtual environment](https://docs.python.org/3/tutorial/venv.html)

## Base environment
```
$ jupyter --version
jupyter core     : 4.5.0
jupyter-notebook : 6.0.1
qtconsole        : 4.5.5
ipython          : 7.8.0
ipykernel        : 5.1.2
jupyter client   : 5.3.3
jupyter lab      : not installed
nbconvert        : 5.6.0
ipywidgets       : 7.5.1
nbformat         : 4.4.0
traitlets        : 4.3.2

$ which jupyter
/Library/Frameworks/Python.framework/Versions/3.7/bin/jupyter
```

## Tweak for JupyterLab
There is one cell which does not work on JupyterLab.  However, this cell can be safely disabled.

If you experience `ERROR: Javascript Error: IPython is not defined` you can remove the following cell, and instead use the menu option `Cell->All Outputs->Toggle Scrolling` to disable auto-scrolling.
```
%%javascript
IPython.OutputArea.prototype._should_scroll = function(lines) {
    return false;
}
```
