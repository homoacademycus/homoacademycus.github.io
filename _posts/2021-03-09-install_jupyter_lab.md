---
{"layout": "post", "categories": "Installation", "title": "install jupyter lab", "feature-img": "assets/img/feature_img.png"}
---
# Jupyter Lab
```
pip install jupyterlab --editable ${PRJ_PATH}
```
a Tornado based HTML Server that serves up an HTML5/Javascript JupyterLab client.

# config
```
jupyter lab paths
jupyter lab --generate-config
```

# run mode
* Core mode(with no extensions)
```
jupyter lab --ip ${ALLOWED_IP} --port ${PORT_JUPYTER} --no-browser --core-mode --log-level='INFO' &
```
run using the JavaScript assets contained in the installed `jupyterlab` Python package. This is the default in a stable JupyterLab release if you have no extensions installed.

* Dev mode(with no extensions)
```
jupyter lab --ip ${ALLOWED_IP} --port ${PORT_JUPYTER} --no-browser --dev-mode --autoreload --debug --log-level='DEBUG' &
```
uses the unpublished local JavaScript packages in the `dev_mode` folder.  In this case JupyterLab will show a red stripe at the top of the page.  It can only be used if JupyterLab is installed as `pip install --editable ${PRJ_PATH}`

* App mode(with a particular set of extensions in $EACH_APP_DIR)
```
jupyter lab --ip ${ALLOWED_IP} --port ${PORT_JUPYTER} --app-dir=${EACH_APP_DIR} --no-browser --log-level='WARN' &
```
allows multiple JupyterLab "applications" to be created by the user 
with different combinations of extensions.
The default application path can be found using `jupyter lab path`.

# SSL/TLS
```
jupyter lab --certfile=${PEM_CERT_PATH}
jupyter lab --keyfile=${PEM_KEY_PATH}
jupyter lab --client-ca=${PEM_CA_PATH} #for SSL/TLS client authentication
```

# matplotlib
- use %pylab or %matplotlib in the notebook to enable matplotlib.


