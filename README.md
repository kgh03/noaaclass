noaaclass
=========

[![License](https://pypip.in/license/noaaclass/badge.svg)](https://pypi.python.org/pypi/noaaclass/) [![Downloads](https://pypip.in/download/noaaclass/badge.svg)](https://pypi.python.org/pypi/noaaclass/) [![Build Status](https://travis-ci.org/ecolell/noaaclass.svg?branch=master)](https://travis-ci.org/ecolell/noaaclass) [![Coverage Status](https://coveralls.io/repos/ecolell/noaaclass/badge.png)](https://coveralls.io/r/ecolell/noaaclass) [![Code Health](https://landscape.io/github/ecolell/noaaclass/master/landscape.png)](https://landscape.io/github/ecolell/noaaclass/master) [![PyPI version](https://badge.fury.io/py/noaaclass.svg)](http://badge.fury.io/py/noaaclass)
[![Supported Python versions](https://pypip.in/py_versions/noaaclass/badge.svg)](https://pypi.python.org/pypi/noaaclass/)

A python library that allow to request images to the NOAA CLASS (Comprehensive Large Array-Data Stewardship System).


Requirements
------------

If you want to use this library on any GNU/Linux or OSX system you just need to execute:

    $ pip install noaaclass

If you want to improve this library, you should download the [github repository](https://github.com/ecolell/noaaclass) and execute:

    $ make deploy


Testing
-------

To test all the project you should use the command:

    $ make test

If you want to help us or report an issue join to us through the [GitHub issue tracker](https://github.com/ecolell/noaaclass/issues).


Example
--------

It can show all the supported products to be subscribed:

```python
import noaaclass
noaa = noaaclass.connect('username', 'password')
print noaa.subscribe.products()
```

Then it can *create new* **subscriptions** to the **gvar_img** product:

```python
import noaaclass
noaa = noaaclass.connect('username', 'password')
data = [
    {
        'id': '+',
        'enabled': True,
        'name': '[auto] sample1',
        'north': -26.72,
        'south': -43.59,
        'west': -71.02,
        'east': -48.52,
        'coverage': ['SH'],
        'schedule': ['R'],
        'satellite': ['G13'],
        'channel': [1],
        'format': 'NetCDF',
    },
    {
        'id': '+',
        'enabled': False,
        'name': '[auto] sample2',
        'north': -26.73,
        'south': -43.52,
        'west': -71.06,
        'east': -48.51,
        'coverage': ['SH'],
        'schedule': ['R'],
        'satellite': ['G13'],
        'channel': [2],
        'format': 'NetCDF',
    },
]
noaa.subscribe.gvar_img.set(data)
```

Also, you can *retrieve all* the subscriptions to the gvar_img product: 

```python
import noaaclass
noaa = noaaclass.connect('username', 'password')
data = noaa.subscribe.gvar_img.get()
```

Last, you can *modify* or *delete* the previous subscriptions:

```python
import noaaclass
noaa = noaaclass.connect('username', 'password')
data = noaa.subscribe.gvar_img.get()
data[1]['name'] = '[auto] name changed!'
data[1]['enabled'] = True
data.pop(0)
data = noaa.subscribe.gvar_img.set(data)
```

About
-----

This software is developed by [GERSolar](http://www.gersol.unlu.edu.ar/). You can contact us to [gersolar.dev@gmail.com](mailto:gersolar.dev@gmail.com).
