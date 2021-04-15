# neon-environment

**INTERNAL USE ONLY:** This GitHub action is not intended for general use.  The only reason why this repo is public is because GitHub requires it.

Loads the values of important JOBRUNNER system environment variables into the
current job as well as the process' environment.  Here's the list of variables
we're currently loading:
```
COMPUTERNAME
NF_REPOS

NF_BUILD
NF_CACHE
NF_CODEDOC
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
GitHub workflows don't seem to load host environment variables into the **env**
context.  This is probably a good idea in general because this prevents workflows
from taking depedencies on the hosting environment.

This is a problem though for neonFORGE projects because our build scripts rely
on environment variables and we've configured these on our self-hosted runners.

This action loads obtains the environment variables above directly via APIs and
for special cases (like COMPUTERNAME) and then adds these to the current job process
as environment variables so they'll be available to all job steps.

This action also sets the MASTER_PASSWORD environment variable to the 
master-password when this is passed.  The MASTER_PASSWORD environment 
variable is used by the underlying Powershell deployment scripts to access the
current user's 1Password secrets on headless jobrunner machines.  We'll
also load the following 1Password secrets into environment variables when
a master-password is passed for convenience:
```
MASTER_PASSWORD

AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
DOCKER_USERNAME
DOCKER_PASSWORD
GITHUB_USERNAME
GITHUB_PASSWORD
GITHUB_PAT
NEONFORGE_USERNAME
NEONFORGE_PASSWORD
NUGET_PUBLIC_KEY
NUGET_VERSIONER_KEY
NUGET_DEVFEED_KEY
```

## Examples

**Load the system environment variables (without master password):**
```
- uses: nforgeio-actions/neon-environment
```


**Load the system environment variables (with master password):**
```
- uses: nforgeio-actions/neon-environment
  with:
    master-password: ${{ secrets.DEVBOT_MASTER_PASSWORD }}
```
