Syncing in Roam can be done by adding a `providers` section `project.config` (or `settings.config`).

The providers section looks like the following:

```
providers:
  Base data:
    cmd: Sync-Basedata.bat
    type: replication
    variables:
      LOCALDATABASE: Roam
```

Each entry under `providers` is a sync button for that project in the Roam sync screen. The options are:

- `cmd` The process to call to run the sync logic.
- `type` must be set to `replication` at the moment
- `variables` environment variables that will be set before running the sync process. You can access these in your sync process.

### No built in sync?
Currently Roam itself doesn't support, or contain, any magic syncing logic.  This is left up to the admin of the project as it varies a lot per site and project.