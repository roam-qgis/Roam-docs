
The recommended way to create IntraMaps Roam projects is to use the Conig Manager. The config manager will allow you to create and manage new projects and forms.

Open the IntraMaps Roam Config Manager using `Roam Config Manager.exe`

The tree view on the left side will list the available projects that Roam has found.  The Roam tree item will display the Roam Config Manager main page with information about Roam itself and how to get started.

![logo](images/config_home.png)

All projects that Roam finds in the `projects` folder will be listed under the Projects item. Selecting a project item will load the project allowing you to configure layers and forms for the project.

![logo](images/config_projectinfo.png)

The map item under each Project folder will load a map view of the QGIS project this Roam project is using. The map view is for a quick reference about the project. 

![logo](images/config_map.png)

Selecting the Forms item will allow you to create a new data entry form for Roam.  Data entry forms are only supported on Point layers currently, however lines and polygons are planned.  If your QGIS project doesn't include any layers a note will be displayed explaining what to do.

![logo](images/config_formlist.png)

![logo](images/config_form.png)

**NOTE** Remember to always save your project using the Save Project button.

# Creating a new project

1. Select the Projects tree item
2. Click the add button ![logo](images/config_add.png)
3. The config manager will ask you for a new folder name. _All Roam projects are stored as folders in the `projects` folder. Folder names must be unique_
4. Roam will create a new project in the `projects` folder.
5. Edit the title and description.

## Adding QGIS layers
1. Select the project node.  Will be selected if you created a new project.
2. Click the Open In QGIS button ![logo](images/config_openqgis.png).  Config manager will watch for changes to the QGIS project.
3. QGIS will be loaded and you are able to add your own layers. _Remember to use the Save.. Project button in QGIS_
4. Tell Config Manager to reload the QGIS project.

## Adding select layers
In Roam select layers are layers that are enabled for selection for using the select tool and will have attribute information displayed in Roam. Any layers not ticked in the Select Layers list will be ignored.

1. Tick the box for each layer that should be selectable  

Data entry forms can also only be added for enabled select layers.  Remember to tick the layer that you would like to do data entry on.

![logo](images/config_selectlayer.png)

## Changing the splash image

Currently there is no way in the config manager to change the project splash however by clicking on the Open Project Folder button

![logo](images/config_openfolder.png)

you can replace the splash.png file with anything you like.  Roam uses splash.png as a convention so remember to always keep that name.

## Adding a new form
1. Select the Forms tree item
2. Select the Add New button ![logo](images/config_add.png)
3. Roam will ask for a new form folder name _Like projects Roam forms are based on folders_
4. Update the name of the form
5. Select the layer for data entry

### Adding attributes to the form
1. Select the Add Attribute button
2. Fill in the relevent fields for each attribute added
3. Select the contol type.

When a attributes control type changes it will also add an extra informtion that control needs.  For example, lists require more information before they can be created in Roam.

![logo](images/config_list.png)

### Previewing the form

Forms can be previewed wihtout having to load Roam.  Simply use the Preview tab on the Form page to enable preview mode.  No defaults are loaded in preview mode but widgets will behave how they would when running Roam.

![logo](images/config_preview.png)

### Changing the form icon

Currently there is no way in the config manager to change the form icon however by clicking on the Form Folder hyperlink 

![logo](images/config_formfolder.png)

you can replace the icon.png file with anything you like.  Roam uses icon.png as a convention so remember to always keep that name.

## Missing UI features

Currently most, but not all, the features that a Roam forms supports is exposed in the config manager.  An example of two that are missing is: remembering the last value for a field, and complex default value types.  By editing the `settings.config` file you can add these features after you have built the form.

The following is an example of a complex default value for a widget.

```
default:
    type: layer-value
    layer: Cadastre
    expression: |
       'within($geometry, buffer($roamgeometry, 10)'
    field: MAP_KEY
```

B
