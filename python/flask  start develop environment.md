See the [torturial](http://flask.pocoo.org/docs/0.12/tutorial/) and [make bigger](http://flask.pocoo.org/docs/0.12/patterns/packages/).


###  make a general flask structure
```
appname/
  appname/
    __init__.py
    static/
    templates/
    views.py
setup.py
```
**setup.py**
```python
from setuptools import setup

setup(
    name='appname',
    packages=['appname'],
    include_package_data=True,
    install_requires=[
        'flask',
    ]
)
```
Now install this package:
```bash
;; -e means --editable
$ pip install -e appname
```
### a start run
Edit the `__init__.py` in `appname/appname`:
```python
from flask import Flask
app = Flask(__name__)

## the views used must imported after the app creation
import appname.views
```
**views.py**:
```python
from appname import app
@app.route('/')
def index():
  return 'hello'
```
Now run:
```bash
$ export FLASK_APP=appname
$ export FLASK_DEBUG=1  ;;enable hot reloading
$ flask run
```

---
**caveat **:
Notice there is circular reference above, that is the side effect to use decorators.
