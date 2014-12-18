Searching can be enabled for each project using the search plugin that is shipped with Roam.  Search is done as a plugin to allow it to be enable or disabled for each project.

### Enable Search

To enable search add the following lines to your projects `project.config`

```
plugins:
   - search_plugin
```

### Search options 

Add entry named `search` and with a sub entry for each layer and columns to `project.config`.  An example of this is

```
search:
  Pipes:
    columns:
    - assetno
  Pits:
    columns:
    - assetno
    - type
```

You may have as many columns that you need per column.

The search index will be created on each project load and can be rebuilt in the UI if needed.

### Searching