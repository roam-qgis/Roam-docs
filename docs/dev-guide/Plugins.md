# Roam Plugins

As of Roam 2.2, Roam will support a basic plugin model to allow adding new panels on the side at run time. 

Plugins live in the `plugins\` folder and are normal Python modules or packages.  The only restriction on naming is the module or package must end with `_plugin`. e.g `plugins\mytest_plugin.py`

A plugin needs to expose two things to work correctly:

1. A `pages()` function which returns a list of QWidgets to use as pages
2. Objects inheriting from a QWidget base to use as a page.

A simple example plugin is as follows:

```
from PyQt4.QtGui import QWidget, QGridLayout, QLabel
from roam.api.plugins import Page

def pages():
    """
    Entry point for exposing pages from the plugin.
    """
    return [SamplePlugin]

class SamplePlugin(QWidget, Page):
    title = "Sample Plugin"

    def __init__(self, api, parent=None):
        super(LineProfile, self).__init__(parent)
        self.setLayout(QGridLayout())
```

`roam.api.plugins.Page` is a shortcut base class that defines default attributes. Your class must provide, or leave them undefined, the following attributes:

* title (string)
* icon (path to icon)
* projectpage (bool)

`projectpage` defines if the page should belong in the upper button group, False if it is a always on panel like Settings, GPS, etc.

## Enabling plugins

Plugins are enabled on a per project basis.  Add:

```
plugins:
- mytest_plugin
```

to enable the above plugin for a given project.  By default all plugins are disabled for each project unless enabled.

When the project is loaded a new button, with the same text as `title`, will be added under Legend.

### Handy functions 

`Page` also has auto connected `selection_changed`, `project_loaded` methods. Simply override and you are good to go:

```
class SamplePlugin(QWidget, Page):
    title = "Sample Plugin"

    def __init__(self, api, parent=None):
        super(LineProfile, self).__init__(parent)
        self.setLayout(QGridLayout())
    
    def selection_changed(self, selection):
        pass

    def project_loaded(self, project):
        pass
```

`selection` is a dict of `QgsVectorLayer: list-of-QgsFeatures`
