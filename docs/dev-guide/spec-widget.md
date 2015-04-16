# The widget config spec

Generally you should use the config manager for creating widgets however the following is the spec for each widget should you need it

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

Each widget type contains its own widget config.  These are found under the ``config:`` key for each widget.

### List
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
```python
config:
   defaultlocation: '%USERPROFILE%\Pictures' # Image picker location
```

### Text, TextBlock

```
NO WIDGET CONFIG
```

### Date
```
NO WIDGET CONFIG
```

### Checkbox

```python
config:
    checkedvalue: 1                 # value to store when checked
    uncheckedvalue: 0               # value to store when unchecked
```
