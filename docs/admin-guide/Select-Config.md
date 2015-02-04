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

### Hiding fields

Fields can be hidden from the info dock using the `hidden` property which takes a list of field names

```
selectlayerconfig:
  pipes:
     hidden:
       - id
       - name
       - photo
```

### SQL Info blocks

SQL Info1 and Info2 blocks are only supported currently on SQL Server and SQLite based layers.

```
selectlayerconfig:
  Inspection:
    info1:
      caption: Inspection
      query: SELECT * FROM Inspection WHERE ID = :mapkey
      type: sql
    info2:
      caption: Inspection Records
      query: SELECT * FROM InspectionRecords WHERE InspectionID = :mapkey AND ParentName = :name
      type: sql
```

Info1 queries will control the first block of information that is displayed when selecting a feature. Normally this is a simple dump of attribute from the feature however by using a info query you are able to control the display. 

A Info2 query can show related records to the selected feature. This is a 1:M result when shown to the user. Any records returned in the info2 query will be shown as a new block of data.

All attributes of the selected feature are passed into the query and can be accessed using the `:` prefix e.g `:type`, `:name` where type and name are field names.

