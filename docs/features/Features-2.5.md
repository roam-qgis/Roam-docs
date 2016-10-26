List of new features and changes in IntraMaps Roam 2.5

[Release Files](https://github.com/DMS-Aus/Roam/releases/tag/v2.5)

#Breaking

- Only load `project.qgs` by default. 

By default Roam will only load `project.qgs` unless `projectfile` is set in `project.config`.  
This will only be issue if you changed the project name after using Roam Config Manager.

#Changes

- [App] New `--profile` command line option to load projects/plugins/logs, etc from profile folder
 See [Profiles](../admin-guide/profiles.md) for more details
- [Project] Allow `[% qgisexpression %]` in info queries.  Will be replaced before the
query is run.
- [Forms] Show GPS marker on map image in drawing widget
- [Forms] New timestamp option for drawing widget. 
- [Forms] Form widget events. Events can be used to change other values or show/hide other controls.
- [Forms] Field expressions can now be run on Capture/Save or Both.
- [Mapping] Snapping enabled on all layers.
- [Mapping] GPS way point markers
- [Mapping] Red highlight for invalid geometry (Doesn't stop the user saving feature)
- [Forms] Generic attachment widget (saved into _attachements, can copy or move attachment to folder)
- [Forms] Add section support
- [Forms] New top down form style.
- [UI] Project download status
- [UI] Move the status bar to the map page only.
- [Config] `image_size` to set fixed image size
- [Config] `smallmode: true` will force toolbars into icon mode at start up.
- [Plugins] Allow plugins to create toolbars in the map widow
- [API] Allow saving features while ignoring form checks. e.g Forced save.
- [App] Plugins folder will be found relative to roam.config
- [API] `Form.new_feature` can take preloaded values.
- [API] Add `zoom_to_feature` method

# Config manager changes:

3126d28 Add new form style option in form config UI
ecb78ce Add search config UI to config manager. Fix search for spaces in columns
c607f62 Add icon picker for form. Update search icon
b65b40a Add html view of project info
8bd4123 Add style widget from QGIS for inline styling
ca147b3 Add plugins node to show installed plugins.
f742584 Rename Default to expression in config manager UI
9a7c093 Add events widget

# Minor Changes:

# Bug fixes

[See](https://github.com/DMS-Aus/Roam/issues?q=milestone%3A2.5+is%3Aclosed) for list of closed tickets.

- Fix error for fields with spaces in info panel.
c9d503d Fix image path loading with space
4ab7c11 Fix #272 - Trim GPS DOP values
e59cb48 Fix #297 - Disable add vertex button with GPS disconnect
0e3ae16 Fix #301 - Fix missing default expression button
ca036a7 Fix #306 - Fix error on no results in search
e95fa92 Fix time selection in date time widget
4357a19 Fix sizing of list view for long entries
f9a4832 Fix image crash. Deep copy widgets config in feature form
418ddaf Fix image from file loading
caded27 Fix missing info dock delete logic
ffcdb3e Use QgsNetworkManager for project download
9600f4e Better field replacement in info panel
07fc057 Fix error on no geom in geom widget
2d3b01f Fix #294 - Crash on missing layer in search
aa1c929 Fix crash on missing geom info
df73d81 Fix show/hide of raster
e72f59c quit project search thread on exit
