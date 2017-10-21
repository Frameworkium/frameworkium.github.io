---
layout: post
title:  "Custom Browser Implementations"
category: wiki
section: 6 - Advanced Usage
order: 12
---

## Custom Browser Implementations

Sometimes, one needs to open browsers and devices with certain capabilities and flags set.
This is achieved in the WebDriver protocol by `DesiredCapabilties`, 
and frameworkium provides a simple mechanism to set these, 
whilst continuing to handle the eventual browser instantiation behind the scenes.

The solution is to create a new Java class extending `AbstractDriver`
somewhere in your test code, which sets up the DesiredCapabilities and WebDriver as you require them;
then reference this class (by name) using the `-DcustomBrowserImpl` parameter at runtime.

### Running chrome in incognito mode example:

Example would be to create the class `ChromeIncognitoImpl.java` somewhere in your test code:

```java
public class ChromeIncognitoImpl extends AbstractDriver {

    @Override
    public DesiredCapabilities getDesiredCapabilities() {
        ChromeOptions options = new ChromeOptions();
        options.addArguments("-incognito");
        DesiredCapabilities capabilities = DesiredCapabilities.chrome();
        capabilities.setCapability(ChromeOptions.CAPABILITY, options);
        return capabilities;
    }

    @Override
    public WebDriver getWebDriver(DesiredCapabilities capabilities) {
        return new ChromeDriver(capabilities);
    }
}
```

Then run your tests with:

`mvn clean verify -DcustomBrowserImpl=ChromeIncognitoImpl`

Whenever `-DcustomBrowserImpl` is provided, the browser parameter defaults to `custom`.

See [the default driver implementations][driver-impl] used in frameworkium-core.
If you create a better default implementation (or just something cool) please submit a pull request.

[driver-impl]: https://github.com/Frameworkium/frameworkium-core/tree/master/src/main/java/com/frameworkium/core/ui/driver/drivers