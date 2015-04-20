# Project update and install

As of 2.4 can now update and install projects if given a URL to an update server.  The config manager can publish projects in the right format to allow Roam the client to download them.  New projects found on the server are offered for install while existing projects can be updated.

## Things you need:

- A webserver (IIS or Apache will be fine)
- Roam config manager on a admin machine

Projects can be updated by using the Roam Config manager to publish a project zip file package to a folder that is also exposed via the webserver

## Steps to publish projects:

- Set publish folder in Config Manager under the Projects node (Deploy Folder). This folder must have write permissions for the current user.
- Create a Virutal Directory in your webserver to this folder
- Create/Manage you project in Roam
- Click the "Publish Install" button in the project page toolbar
or
- Click the "Publish Update" button to create a update only package (no data included)

The version of the project is increased on each save/publish. Roam will check the version installed local to the version on the server to see if a new version needs to be installed.

**Note**: Currently projects must include at least a single install package.

## Setting the update server in Roam

- Add the URL of the server into the **Settings** page of Roam. e.g `http:\\my_server\RoamProjects`
- Select the **Project** tab for Roam to search for new/updated projects.

**Note**: Currently Roam searches for new packages in the background and doesn't give a lot of error reporting if something does go wrong. Errors are logged in the \log folder, check there if your projects are not showing up.

## Updating or Installing projects

New projects found on the server are shown with an install button next to there project entry.  Installing a project will download the project package and extract it into the local folder.

It is possible to update and install packages will using another project as all updating/installing is done in the background without affecting the currently running projects.  Connection to server required of course.

Roam will also run and install the update back 


### Internal Workings

At the current time Roam Config Manager will create a `projects` folder in the publish folder on the server.  It will also create and manager a `roam.txt` file. `roam.txt` contains the information about the projects on the server.  The config manager will manage this file for you. You should never had to edit it by hand.

Here is an example of a `roam.txt`:

```yaml
projects:
  !!python/unicode 'Sample':
    description: Sample capture project including a basic inspection form and searching.
    name: !!python/unicode 'Sample'
    title: Sewer Access Pit Sample
    version: 2
```

### DMS Demo projects

Demo projects from DMS can be installed into Roam using the following update server `http://demo.mapsolutions.com.au/RoamDemos/`
