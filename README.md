# neon-environment
GitHub Action that loads JOBRUNNER system environment variables into the current job.

These are the system variables currently loaded by the action:
```
NF_BUILD
NF_CACHE
NF_CODEDOC
NF_REPOS
NF_ROOT
NF_SAMPLES_CADENCE
NF_SNIPPETS
NF_TEMP
NF_TEST
NF_TOOLBIN

NC_ACTIONS_ROOT
NC_BUILD
NC_CACHE
NC_NUGET_DEVFEED
NC_NUGET_VERSIONER
NC_REPOS
NC_ROOT
NC_TEMP
NC_TEST
NC_TOOLBIN
```

## Examples

Load the system environment variables
```
- uses: nforgeio-actions/neon-environment
```
