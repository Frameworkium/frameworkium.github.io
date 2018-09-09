---
layout: post
title:  "Command Line Options"
category: wiki
section: 2 - Basics
order: 1
---
Tests can be executed by running `mvn clean verify`.
This can be followed by any properties, in the form `-DpropertyName=value`,
you wish to specify.

**See also** the ["Using Config files..."](Config_Files.md) entry for using config files
to provide a subset of these params instead

## General

Property | Description | Values | Default
-------- | ----------- | ------ | -------
`test`| The test class, or comma separated list of test classes, to run. Can include wildcards. | e.g. `MyTest*` | All tests
`threads`| The number of threads to use. | e.g. `3` | 1
`reuseBrowser` | Will re-use existing browsers rather than starting a new instance for each test. | `true` or `false` |  `false`
`groups`| The TestNG test groups which you wish to run. | e.g. `checkintest` | All groups
`build`| The build version or app version to log to Sauce Labs, BrowserStack, or Capture. | e.g. `build-1234` | none
`proxy` | Proxy server to be used from Selenium and REST API requests. | `system`, `autodetect`, `direct` or `http://{hostname}:{port}`, e.g. `http://10.3.2.22:80` | none
`maxRetryCount` | Additional attempts to retry a failed test. | e.g. `3` | 1

## Browser Properties/Capabilities

Property | Description | Values | Default
-------- | ----------- | ------ | -------
`browser`|  The browser on which you wish to run the tests. |`firefox`, `chrome`, `safari`, `ie`, `opera`, `legacyfirefox`,`electron`,`custom` | `firefox`
`maximise`| Maximise browser on opening (if possible). | `true` or `false` | `false`
`resolution`| Set browser dimensions to specific setting (if possible). | e.g. `1024x543` | none
`chromeUserDataDir`| Removed in v3.0.0. See `customBrowserImpl` below for preferred method. | e.g. `path/to/chrome_user_data_dir` | none
`customBrowserImpl`| Allows users to specify classname (fully qualified name in v3.0.0) of their own browser implementation, for example for specifying a custom set of `Capabilities`. | e.g. `ChromeIncognitoBrowserImpl` or since v3.0.0 `my.package.ChromeIncognitoBrowserImpl` | none
`headless`| Allows users to run Chrome or Firefox in a headless environment | `true` or `false` | `false`

## Remote Grids. Devices and Platforms

No defaults.

Property | Description | Values
-------- | ----------- | ------
`gridURL`| The URL of your Selenium Grid hub. | e.g.`http://localhost:4444/wd/hub` - NB `/wd/hub` is required!
`browserStack`| Must be set to `true` if you wish to run on BrowserStack. | `true` or `false`
`sauce`| Must be set to true if you wish to run on Sauce Labs. | `true` or `false`
`browserVersion`| The browser version on which you wish to run the tests. Only used when running remotely e.g. on Selenium Grid, Sauce Labs or BrowserStack. | e.g. `8.0`
`platform`| The platform on which you wish to run the tests. Only used when running remotely. To be specified instead of 'os' when running with BrowserStack. | e.g. `windows`, `ios`, `android`, `OSX`
`platformVersion`| The platform version on which you wish to run the tests. Only used when running remotely. To be specified instead of 'os_version' when running with BrowserStack. | e.g. `5.0`
`device`| The device on which you wish to run remote tests. If not using SauceLabs or BrowserStack, can be specified with the `-Dbrowser=chrome` parameter to instigate a Chrome browser emulator of the specified device. |`iPhone`, `iPad`, `iPhone Retina 4-inch`, `Galaxy S4`, etc.
`applicationName`| Specify applicationName parameter for a grid run.| e.g. `windows7_32bits_firefox`
`videoCaptureUrl`| Enable video capture using Grid plugins. Usage of video capture is generic as possible. All grid plugins, such as Selenium Grid Extras, capture videos by the WebDriver session ID.| e.g. `http://localhost:3000/download_video/%s.mp4`
`appPath`| The path to the apk file to be used in Sauce Labs. It is also used as the `app` desired capability of the supported [WinAppDriver](https://github.com/Microsoft/WinAppDriver). | e.g. `/home/dev/android/build/newapp_1.2.5.apk` for SauceLabs or `Microsoft.WindowsAlarms_8wekyb3d8bbwe!App`, or `C:\Windows\System32\notepad.exe` for the WinAppDriver.

### Remote Supported Devices/Platforms

- [BrowserStack](https://www.browserstack.com/list-of-browsers-and-platforms)
- [SauceLabs](https://saucelabs.com/platforms)

## Jira/Zephyr/Test Result Logging Integrations

No defaults.

Property | Description | Values
-------- | ----------- | ------
`jiraURL`| The base URL of the JIRA instance you want to use | e.g. `http://jira:8080`
`jiraUsername`| The JIRA user you want to use | e.g. `JBloggs`
`jiraPassword`| The JIRA user's password | e.g. `password`
`jqlQuery`| the JQL query to look up the JIRA tests to run (the results of the query will be looked up against the `@Issue` annotations on tests). | e.g. `(priority=1 and component=Admin) or issueKey=JIRA-123`
`jiraResultFieldName`| The Jira field name to attempt to log results to for the specified `@Issue`. The values to change the field to are specified in the Jira config file. Useful if you're using a Jira field to mark the test result. | e.g. `Test Result`
`jiraResultTransition`| If specified, will attempt to transition the `@Issue` specified through the transitions specified in the Jira config. Useful if using a customised Jira workflow for managing test results. | any value
`resultVersion`| The 'Version' to mark the test execution against in Zephyr for JIRA (requires ZAPI). | e.g. `App v1.1.2`
`zapiCycleRegEx`| If the Zephyr test cycle name contains this string test results will be logged against the matching cycles. | e.g. `firefox` or `my-special-cycle`

## Spira Integration

No defaults.

Property | Description | Values
---------|-------------|-------
`spiraURL`| The base URL of the Spira instance you want to use | e.g. `http://spira:8080`
 
## Capture Integration

A Capture server is a custom server developed to allow Frameworkium tests to 
send screenshots for each step they are executing.
All three need to be defined for the integration to work correctly.

No defaults.

Property | Description | Values
---------|-------------|-------
`captureURL`| The base URL of the Capture instance you want to automatically send screenshots and step information to. | e.g. `http://capture/`
`sutName`| The name of the system under test (SUT) to be presented in the Capture dashboard. | e.g. `My App`
`sutVersion`| The release version to appear on the Capture dashboard. | e.g. `1.2.5`

## Examples

Running tests using Firefox:

```bash
mvn clean verify
```

Running web tests using Chrome:

```bash
mvn clean verify -Dbrowser=chrome
```

Running web tests on Firefox 58.0.1 with Selenium Grid:

```bash
mvn clean verify -Dbrowser=firefox -DbrowserVersion=58.0.1 -DgridURL=http://localhost:4444/wd/hub
```

Running test methods which match the pattern`testM*`on Firefox with Selenium Grid and Capture:

```bash
mvn clean verify -Dtest=TestClass#testM* -Dbrowser=firefox -DgridURL=http://grid:4444/wd/hub -DsutName="My Project" -DsutVersion="0.0.1" -DcaptureURL=http://capture/
```

Running mobile web tests on Chrome, using its device emulation:

```bash
mvn clean verify -Dbrowser=chrome -Ddevice="Apple iPad 3 / 4"
```

Running mobile web tests on BrowserStack Win XP Firefox 33:

```bash
export BROWSER_STACK_USERNAME=<username>
export BROWSER_STACK_ACCESS_KEY=<access_key>
mvn clean verify -DbrowserStack=true -Dbrowser=firefox -DbrowserVersion=57.0 -Dplatform=Windows -DplatformVersion=XP
```

Running mobile web tests on Sauce Labs iOS 8.0 iPad Simulator:

```bash
export SAUCE_USERNAME=<username>
export SAUCE_ACCESS_KEY=<access_key>
mvn clean verify -Dsauce=true -Dplatform=ios -Dbrowser=safari -DplatformVersion=8.0 -Ddevice="iPad Simulator"
```

Running mobile web tests on BrowserStack iOS iPad Air (real device):

```bash
export BROWSER_STACK_USERNAME=<username>
export BROWSER_STACK_ACCESS_KEY=<access_key>
mvn clean verify -DbrowserStack=true -Dbrowser=ios -Ddevice="iPad Air"
```

NB - platform and platformVersion (os & os_version in BrowserStack config) are 
not required or supported when running on mobile devices

Running mobile app tests on Sauce Labs Android Emulator:

```bash
export SAUCE_USERNAME=<username>
export SAUCE_ACCESS_KEY=<access_key>
mvn clean verify -Dsauce=true -Dplatform=android -DappPath=<path_to_.apk>
```

Run regression tests (as marked in JIRA with the label REGRESSION) and log test 
results against the v1.1.2 version in JIRA:

```bash
mvn clean verify -Dbrowser=firefox -DjiraURL=http://jira:8080 -DjiraResultVersion=v1.1.2 -DjqlQuery="labels=REGRESSION"
```

For full lists of platforms/browsers supported see:
[BrowserStack](https://www.browserstack.com/list-of-browsers-and-platforms?product=automate) 
and [SauceLabs](https://saucelabs.com/platforms/) platform lists.
