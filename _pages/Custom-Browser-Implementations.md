---
layout: post
title:  "Custom Browser Implementations"
category: wiki
section: 6 - Advanced Usage
order: 12
---

## Custom Browser Implementations

Sometimes, one needs to open browsers and devices with certain capabilities and
flags set that are not already part of Frameworkium.
This is achieved in the WebDriver protocol by `Options` for each browser
e.g. `ChromeOptions`, `FirefoxOptions`, these implement the `Capabilities` interface.
Frameworkium provides a simple mechanism to set these, 
whilst continuing to handle the eventual browser instantiation behind the scenes.

The solution is to create a new Java class extending `AbstractDriver` somewhere
in your test code, which sets up the `Capabilities` and `WebDriver` as you require them;
then reference this class (by name) using the `-DcustomBrowserImpl` parameter at runtime.

### Running Chrome in Incognito mode example

Example would be to create the class `ChromeIncognitoImpl.java` somewhere in your test code:

```java
public class ChromeIncognitoImpl extends ChromeImpl {

    @Override
    public Capabilities getDesiredCapabilities() {
        ChromeOptions chromeOptions = super.getCapabilities();
        chromeOptions.addArguments("--incognito");
        return chromeOptions;
    }

    @Override
    public WebDriver getWebDriver(Capabilities capabilities) {
        return super.getWebDriver(capabilities);
    }
}
```

Then run your tests with:

`mvn clean verify -DcustomBrowserImpl=ChromeIncognitoImpl`

Since 3.0.0:

`mvn clean verify -DcustomBrowserImpl=my.package.ChromeIncognitoImpl`

### Using Appium

As of version 3.0.0 Appium is no longer part of core. However you can easily use
it by implementing a CustomBrowserImpl.

```java
import com.frameworkium.core.ui.driver.AbstractDriver;
import io.appium.java_client.windows.WindowsDriver;
import io.appium.java_client.windows.WindowsElement;
import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;
import org.openqa.selenium.*;

import static com.frameworkium.core.common.properties.Property.*;

public class WinAppDriverImpl extends AbstractDriver {

    protected static final Logger logger = LogManager.getLogger();

    @Override
    public Capabilities getCapabilities() {
        logger.info("Creating capabilities for WinAppDriverImpl");
        MutableCapabilities mutableCapabilities = new MutableCapabilities();
        mutableCapabilities.setCapability("platformName", "Windows");
        if (PLATFORM_VERSION.isSpecified()) {
            mutableCapabilities.setCapability(
                    "platform", "Windows " + PLATFORM_VERSION.getValue());
            mutableCapabilities.setCapability(
                    "platformVersion", PLATFORM_VERSION.getValue());
        } else {
            String message = "Platform version needs to be specified when using Windows";
            logger.error(message);
            throw new IllegalArgumentException(message);
        }

        if (DEVICE.isSpecified()) {
            mutableCapabilities.setCapability("deviceName", DEVICE.getValue());
        } else {
            mutableCapabilities.setCapability("deviceName", "WindowsPC");
        }

        if (APP_PATH.isSpecified()) {
            mutableCapabilities.setCapability("app", APP_PATH.getValue());
        } else {
            mutableCapabilities.setCapability("app", "Root");
        }

        return mutableCapabilities;
    }

    @Override
    public WebDriver getWebDriver(Capabilities capabilities) {
        return new WindowsDriver<WindowsElement>(capabilities);
    }

}
```

You will also need to add the Appium dependency to your `pom.xml` file.

```xml
<dependency>
  <groupId>io.appium</groupId>
  <artifactId>java-client</artifactId>
  <version>6.1.0</version>
</dependency>
```

If you need access to the Appium Driver you can use the following:

```java
if (driver instanceof AppiumDriver) {
    return (AppiumDriver) driver;
} else {
    throw new IllegalStateException(wd + " is not an instance of AppiumDriver");
}
```

Whenever `-DcustomBrowserImpl` is provided, the `-Dbrowser` parameter defaults to `custom`.

See [the default driver implementations][driver-impl] used in frameworkium-core.
If you create a better default implementation please submit a pull request.

[driver-impl]: https://github.com/Frameworkium/frameworkium-core/tree/master/src/main/java/com/frameworkium/core/ui/driver/drivers