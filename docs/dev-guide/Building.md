If you are planning on doing any development work on Roam or are wanting to stay current with recent changes you will need to build from source.

# Setting QGIS path

First set your QGIS home path and version in `scripts\setenv.bat`.  The default will look in `C:\OSGeo4W`
```
...
SET OSGEO4W_ROOT=C:\OSGeo4W
SET QGISNAME=qgis
SET QGIS=%OSGEO4W_ROOT%\apps\%QGISNAME%
set QGIS_PREFIX_PATH=%QGIS%
...
```

# Build environment setup

IntraMaps Roam is complied and built as a standalone Python application.  In order to do this we need to download and install a few tools into QGIS Python install, mainly py2exe.

You will need:

- [Visual Studio C++ 2008](http://download.microsoft.com/download/A/5/4/A54BADB6-9C3F-478D-8657-93B3FC9FE62D/vcsetup.exe) (This is for the C compiler for py2exe)
- [QGIS 32bit OSGeo4W](http://download.osgeo.org/osgeo4w/osgeo4w-setup-x86.exe)

### Will 64bit QGIS work?

Maybe I haven't tried but you are welcome.

### The easy way

1. Download and install Visual Studio C++ Express
2. Install QGIS using OSGeo4W
3. Update you QGIS path in `scripts\setenv.bat`
2. Run ``scripts\setupdev.bat``

``setupdev.bat`` will download and install py2exe, easy_install, pip, and anything else the project needs.  

**INSTALL NOTE:**  If you get a ``ValueError`` when running ``setupdev.bat`` sometimes Python can't run the visual studio batch file.  Simply run `C:\Program Files (x86)\Microsoft Visual Studio 9.0\Common7\Tools\vsvars32.bat` in the shell
before running ``setupdev.bat``

# Creating the binary package

IntraMaps Roam is built as a standalone fully packaged Python application using py2exe on Windows.  Once built as a binary package QGIS is not required on the users machine.

1. Run `package.bat`
2. Errors will be in the shell, everything else in package.log
3. Final output will be in `dist\`
4. Everything in `dist\` can be copied to the users machine and installed without needing QGIS.

# Release package

Running `scripts\make_release.bat` will creata a self extracting installer and zip file in the `release` folder
