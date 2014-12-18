# Project Format

IntraMaps Roam projects all live in the ``projects\`` folder in the Roam install location.

An example project folder layout looks like this:

Note: Project folders should have no spaces or special characters in the name.  Will be imported by Python.

Each project folder should contain the following:

	__init__.py
	settings.config
	splash.png
	1 QGIS project file (any name)
	form folders
	Example Project folder.


Roam will pick up the first QGIS project (.qgs) file in the folder and load it into the map.  All form configuration and any other Roam configuration for the project is found in ``settings.config``.

A form folder must have a matching name in ``settings.config`` and contain the following files:

	__init__.py
	icon.png
	.\help\ (optional)

# Settings.Config

The project settings.config file contains all the configuration that Roam needs for the form.  The file format is YAML.

**NOTE: YAML is sensitive to tabs. [Why!?](http://www.yaml.org/faq.html) Make sure you are using spaces to indent. Also make sure you use a decent editor (Notepad++, Sublime, Vim, VS, etc) anything besides Notepad really, but you already do that.**

## Title and Description

The minimum data the settings.config file must contain is a title and description:

```python
title: 'Tree Inspection (Sample)'
description: Sample tree inspection module
```

If a settings.config only contains a title and description,  a project with no forms will be created.  A project with no forms can still be loaded and viewed.  Handy for a info only project.

## Select Layers

To control which layers will show up in the info panel when using the select tool you can add a selectlayers: key.  

```python
title: 'Tree Inspection (Sample)'
description: Sample tree inspection module

# List each layer that can be "selected". 
# The order is respected in the info panel. 
# Any layers with spaces in their names must be wrapped in ' '
selectlayers:
    - Trees
    - 'Property Boundaries'
    - 'Main Roads'
```

If this is not found in the ``settings.config`` file all layers will be selectable and the order is based on the project file order.

## Providers

Used to specify batch scripts which should be called from the sync page.

```providers:
  Trees:
    cmd: Sync-Inspections.bat
    type: replication
```

Output will be caught and displayed on the sync page.

## Forms

All forms are found under the ``forms:`` key.  The basic layout of form config is:

```python
forms:
  trees:                       # Must have a matching folder and unique
    layer: Trees               #Layer name in QGIS project
    label: Tree Inspection     # Label shown in Roam interface
    type: 'auto'               # Form type. Can be 'auto'
    display: |                 # Display expression show in the info panel
      [% "Botname" %]
    widgets:                   # List of widgets defined for this form.
      .... # Widgets listed here.
```

The ``layer:`` key tells roam which layer this form is bound to. One layer can have many forms in Roam.  This allows for a project to have different views (forms) into the data model.   An example might be a asset table where all the different asset type information is in a single table rather then different layers.  You could then have a Trees form, and also a Bin form which both point to the same layer just different columns. 

An example of this setup might be:

```python
forms:
  Bins:
    layer: Assets
    label: Bin  
    type: 'auto'               
    display: |                 
      [% "Botname" %]
    widgets:                   
      .... # Widgets listed here.
  Trees:
    layer: Assets
    label: Tree    
    type: 'auto'               
    display: |                 
      [% "Botname" %]
    widgets:                   
      .... # Widgets listed here.
```

This would then show up as two different forms.

# Widgets 

All forms in Roam are made up of widgets. Most widgets allow for data entry, some are just visual (group box, horizontal line, etc).   Each widget contains its own config section under the `config:` key. 

Note: Inline comments marked as #
Note: The order of the keys do not matter

```python
forms:
  Trees
    layer: MyLayer
    label: UI Label
    type: 'auto'
    widgets:
	- widget: {widgettype}              
	  field: {fieldname}:               # Only one entry per field
	  name: 'Display Name'              # optional - default {fieldname}
	  hidden: false                     # optional - default false
	  read-only-rules: [editing]        # optional. Values are: always, insert, editing
	  required: false                   # optional - default false
	  default: {value}                  # optional - See default section
	  rememberlastvalue: true           # optional - Adds option to remember values
	  config:                           # Optional for some widget
	     {widget config}                # Config for the widget
```

## Default Values 

Widgets may also contain a default values.

```python
default: {value}

default: %USERNAME%                 # All environment variables are expanded.

default: '[% $now %]'               # QGIS expression are enclosed in [% %]

default: |                          # Or as a yaml literal if quotes need to be used.
  [% format_date($now, 'ddMMyyyyhhmmss') %]

# A default value with a sub key of type: layer-value will pull the first record it finds
# which matches the expression from the layer after layer:. 
# Note: Will only search features in view.  
# $roamgeometry is the geometry of the current captured feature.
# The expression can also access fields of the search layer
default:
    type: layer-value
    layer: Cadastre
    expression: |
       'within($geometry, buffer($roamgeometry, 10)'
    field: MAP_KEY
```

## Widget Types

Supported widget types are:

 - List
 - Image
 - Text
 - TextBlock
 - Date
 - Checkbox
 - Widget Configs

Each widget type contains its own widget config.  These are found under the ``config:`` key for each widget.

### List
![list](images/list.png)

List based on string list:

```python
config:
  allownull: false                  # optional - default
  list:
    items:
    - 'Sub Type;Desc '              # ; can be used to show description
    - 'Sub Type2;Test'
    - 'Sub Type3'
```

List based on layer:

```python
config:
  allownull: false
  layer:
    layer: 'MyLayer'
    key: 'COL1'                     # Column for display
    value: 'COL2'                   # Value that is stored in the layer
    filter: |                       # Optional - | means literal string. This must be used.
	"name" = 'nw'               # Expression must be on new line nested after |
```

### Image
![list](images/photo.png)

```python
config:
   defaultlocation: '%USERPROFILE%\Pictures' # Image picker location
```

### Text, TextBlock

```
NO WIDGET CONFIG
```

### Date
![list](images/date.png)
```
NO WIDGET CONFIG
```

### Checkbox

```python
config:
    checkedvalue: 1                 # value to store when checked
    uncheckedvalue: 0               # value to store when unchecked
```

### Examples

Example list:

```python
widgets:
  - widget: List
    field: Asset_Sub_Type
    required: false
    name: 'Asset Sub Type'
    default: 'Sub Type2'
    config:
      allownull: false
      orderbyvalue: false
      list:
	items:
	- 'Sub Type;Desc '
	- 'Sub Type2;Test'
	- 'Sub Type3'
```

Example checkbox:

```python
widgets:
  - widget: Checkbox
    field: has_powerlines:
    required: false
    name: 'Is there powerlines?'
    config:
	checkedvalue: True
	uncheckedvalue: False
```
