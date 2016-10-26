## Roam Profiles

Starting Roam with the `--profile` option allows you to control the folder that Roam and Config Manager will load 
settings and projects from.

Using this it is possible to setup different folders for different "profiles" with their own projects and plugins, keeping
them isolated.

Roam will make the profile folder with the right layout to run.

Usage: `roam.exe --profile C:\temp\testing`

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

