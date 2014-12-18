All forms in Roam are made up of widgets. Most widgets allow for data entry, some are just visual (group box, horizontal line, etc).   Each widget contains its own config section under the `config:` key. 

Widgets found in each forms `form.config` file under the `widgets` header

All widgets can be configured using the config manager. 

Note: Inline comments marked as #
Note: The order of the keys do not matter

```python
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

Supported widget types are:

 - List/Multi List
 - Option Row
 - Number/Number Double
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
