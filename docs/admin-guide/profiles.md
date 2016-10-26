## Roam Profiles

Starting Roam with the `--profile` option allows you to control the folder that Roam and Config Manager will load 
projects/plugins/roam.config, etc from.

Using this it's possible to setup different folder for different "profiles" with their own projects and plugins.

Roam will make the profile folder and any nested folders and config it needs

`roam.exe --profile C:\temp\testing`

### Example

This can be used to have test vs production style setup

`roam.exe --profile C:\temp\test`

will make the following setup:

- C:\temp\test\projects\*
- C:\temp\test\plugins\*
- C:\temp\test\logs\*
- C:\temp\test\roam.config


`roam.exe --profile C:\temp\prod`

- C:\temp\prod\projects\*
- C:\temp\prod\plugins\*
- C:\temp\prod\logs\*
- C:\temp\prod\roam.config

