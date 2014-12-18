# Roam Events

Roam events is a global API object which gives you access to common events within Roam.  The primary use of the RoamEvents object is for use with plugins or feature forms.

All events can be accessed by importing `RoamEvents` using `from roam.api import RoamEvents`

The RoamEvents class has the following methods:

```
"""
Emit when you need to open a image in the main window

Usage:
	openimage.emit(QImage)
"""
openimage = pyqtSignal(object)
```

```
"""
Emit to open a url
"""
openurl = pyqtSignal(QUrl)
```

```
"""
Load a form into the data entry tab.
:param form: The Form to load. See roam.project.Form
:param feature: Feature to load
:param editmode: Open in edit mode
:param clearcurrent: Clear the current stack of open widgets.
"""
def load_feature_form(self, form, feature, editmode, clearcurrent=True, callback=None):
```

```
"""
Emit when you need to open the on screen keyboard
"""
openkeyboard = pyqtSignal()
```

```
"""
Called when the selection is cleared
"""
selectioncleared = pyqtSignal()
```

```
"""
Called when the selection is changed
"""
selectionchanged = pyqtSignal(dict)
```

```
"""
Called when a new project is loaded
"""
projectloaded = pyqtSignal(object)
```

```
"""
Called when a new project is loaded
"""
projectClosed = pyqtSignal(object)
```

```
"""
Close the current open project
"""
def close_project(self, project=None):
```

```
"""
Raise a message for Roam to show.
:param title: The title of the message.
:param message: The message body
:param level: 
:param time: How long the message should be shown for.
:param extra: Any extra information to show the user on click.
"""
def raisemessage(self, title, message, level=0, duration=0, extra=''):
```
