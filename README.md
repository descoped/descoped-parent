# Descoped Parent POM

[![Build Status](https://travis-ci.org/descoped/descoped-parent.svg?branch=master)](https://travis-ci.org/descoped/descoped-parent)

mvn clean deploy for snapshots

mvn release:clean release:prepare release:perform -DreleaseVersion=1 -DdevelopmentVersion=1-SNAPSHOT

Repo must be be configured with AllowRedeploy

Travis-CI and secret must be fixed, then snapshots will be deployed for each build

Then figure out how to use Maven Central. Not a priority, but may be useful in the future.

git config --global credential.helper osxkeychain
ssh-add -K
