# Release

This document outlines how we handle release management.

## Pre-requisites

* Nexus must be configured with Repo for Releases and Snapshots, where the option `AllowRedeploy` must be set. If not, you will get a HTTP Error Code 400 Bad Request
* Configure Maven locally in `~/.m2/settings.xml`:
```xml
<servers>
        <server>
            <id>descoped</id>
            <username>${env.CI_NEXUS_USER}</username>
            <password>${env.CI_NEXUS_PWD}</password>
        </server>
        <server>
            <id>descoped-snapshots</id>
            <username>${env.CI_NEXUS_USER}</username>
            <password>${env.CI_NEXUS_PWD}</password>
        </server>
</servers>
```
* Set up environment vars `CI_NEXUS_USER` and `CI_NEXUS_PWD` in either `.profile` or `.bash_profile`

## Configure Git and Keystore on MacOS

On MacOS, Git will prompt you for password repeatedly. A solution is to add git to the keystore: 

* `git config --global credential.helper osxkeychain`
* `ssh-add -K`

## Do Snapshot

`git pull`

`mvn clean deploy for snapshots`

## Do Release

Make sure all pre-requisites and that all files are committed before you release.

`git pull`

Make sure all files are up-to-date.

`mvn release:clean release:prepare release:perform -DreleaseVersion=1.0.0 -DdevelopmentVersion=1.0.1-SNAPSHOT`

### Project checklist order:

* parent
* descoped-logger
* descoped-container
* descoped-testutils
* descoped-support
* descoped-web
* descoped-rest
* descoped-mvc
* descoped-hystrix-http
* mojo


### Revert when something goes wrong

`git reset --hard origin/master`

`git pull`

`git status`

## Travis

`travis encrypt "<slackgroup>:<secret>" --add notifications.slack`

`travis encrypt CI_NEXUS_USER='<user>' --add`
`travis encrypt CI_NEXUS_PWD='<pwd>' --add`

