# Feature Form API

Each form form in Roam has the ability to have custom logic defined behind the form.  The feature form has the following methods that can be used for hooks.

Before any custom logic can be used it must be registered with the Roam form object.  This is normally done in the forms folder `__init__.py` file like this:

```
from form import Form


def init_form(form):
    # Register the class Form with the current form.
    # Form can be used to override/add logic to the form in Roam
    form.registerform(Form)
```

When a form is created in Roam a `form.py` will also be created with the following:

```
from roam.api import FeatureForm, RoamEvents


class Form(FeatureForm):
    def __init__(self, *args, **kwargs):
        super(Form, self).__init__(*args, **kwargs)

    def uisetup(self):
        pass

    def load(self, feature, layers, values):
        """
        Called before the form is loaded. This method can be used to do pre checks and halt the loading of the form
        if needed.

        Calling self.cnacelload("Your message") will stop the opening of the form and show the message to the user.

            >>> self.cancelload("Sorry you can't load this form now")

        You may alter the values given in the values dict. It will be passed to the form after this method returns.
        """
        pass

    def loaded(self):
        """
        Called after the form is loaded into the UI.
        """
        pass

    def featuresaved(self, feature, values):
        """
        Called when the feature is saved in QGIS.

        The values that are taken from the form as passed in too.
        :param feature:
        :param values:
        :return:
        """
        pass

    def featuredeleted(self, feature):
        """
        Called once the feature has been delete from the layer.
        :param feature:
        """
        pass

    def accept(self):
        """
        Called before the form is accepted.  Override this and return False to cancel the accepting of the form.
        :return:
        """
        return True
```

You can also overload the save and delete methods:

```
def delete(self):
    # Add override delete logic	
    super(Form, self).delete() 
```

**Note**: When overriding delete logic it is always a good idea to call the base delete method as this handels a lot of the logic for you.  If you wish to raise a error in `delete` you can call `FeatureDeleteExpection.not_saved(message)` to cancel and let the user know.

```
def save(self):
   # Add override save logic
   super(Form, self).save()
```

**Note**: When overriding save logic it is always a good idea to call the base save method as this handels a lot of the saving logic for you.  If you wish to raise a error in `save` you can call `FeatureSaveExcpection.not_saved(message)` to cancel and let the user know.

## Accessing widgets

All widgets that have been created on the form via Roam can be accessed via `self.boundwidgets`:

```
name = self.boundwidgets['name']
```

Setting values can be done via `value()` and `setvalue()` functions

```
self.boundwidgets['name'].setvalue("Hello World")
self.boundwidgets['name'].value()
```

Widgets also have a generic `valuechanged` signal

```
self.boundwidgets['name'].valuechanged.connect(self.handler)

def handler(self, value):
    print value
```

Generally you should connect to the `valuechanged` in the forms `uisetup` method in order to correctly handle when the values are loaded into the form
