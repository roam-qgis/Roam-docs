Select config is a advanced section you can add to the `project.config` file, no UI as yet, to control how the select layers behave and what tools you can use.

A select layer config entry looks like this

```
selectlayerconfig:
  {layer name}:
    {properties}
```

`{layer name}` must match a active select layer name

### Setting active tools

You can control the tools that are available for a given layer with the following config. 
```
selectlayerconfig:
  pipes:
    tools:
    - edit_attributes
    - edit_geom
    - capture
```

* `edit_attribute` enable edit attribute support
* `edit_geom` enable edit geometry support
* `capture` enable capture support

### Info 1 and Info 2

Info1 and Info2 blocks are only supported currently on SQL Server based layers and are a growing feature so documentation is not complete yet.


```
selectlayerconfig:
  Inspection:
    info1:
      caption: Inspection
      connection: from_layer
      query: SELECT * FROM Inspection WHERE ID = :mapkey
      type: sql
```