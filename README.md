# Descoped Parent POM

[![Build Status](https://travis-ci.org/descoped/descoped-parent.svg?branch=master)](https://travis-ci.org/descoped/descoped-parent)

Repo is configured with AllowRedeploy that fixes 400 bad request.

mvn clean deploy for snapshots

mvn release:clean release:prepare release:perform -DreleaseVersion=1 -DdevelopmentVersion=2-SNAPSHOT

git config --global credential.helper osxkeychain
ssh-add -K
