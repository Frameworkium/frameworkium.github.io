---
layout: post
title:  "Using Config Files Rather than Command Line params"
category: wiki
section: 6 - Advanced Usage
order: 0
---

Rather than providing all of the details in the command line, you can instead 
create config files (in your `resources` folder) to store common configurations.

An example would be:

`/resources/config/FirefoxGrid.properties`:

```
applicationName=
appPath=
browser=Firefox
browserStack=
browserVersion=
build=
captureURL=
customBrowserImpl=
device=
gridURL=http://localhost:4444/wd/hub
headless=
jiraPassword=
jiraResultFieldName=
jiraResultTransition=
jiraURL=
jiraUsername=
jqlQuery=
maximise=true
maxRetryCount=2
platform=
platformVersion=
proxy=
resolution=
resultVersion=
reuseBrowser=
sauce=
spiraURL=
sutName=
sutVersion=
threads=
videoCaptureUrl=
zapiCycleRegEx=
```

Colon (:) can also be used as a separator.

`/resources/config/FirefoxGrid.properties`:

```
applicationName:
appPath:
browser: Firefox
browserStack:
browserVersion:
build:
captureURL:
customBrowserImpl:
device:
gridURL: http://localhost:4444/wd/hub
headless:
jiraPassword:
jiraResultFieldName:
jiraResultTransition:
jiraURL:
jiraUsername:
jqlQuery:
maximise: true
maxRetryCount: 2
platform:
platformVersion:
proxy:
resolution:
resultVersion:
reuseBrowser:
sauce:
spiraURL:
sutName:
sutVersion:
threads:
videoCaptureUrl:
zapiCycleRegEx:
```

and you'd then use this config file by running:

```bash
mvn clean verify -Dconfig=FirefoxGrid.properties
```
