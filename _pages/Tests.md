---
layout: post
title:  "Tests"
category: wiki
section: "2 - Basics"
order: 3
---
## BaseTest

Test classes must extend `com.frameworkium.core.ui.tests.BaseTest`.
This handles the `setup` and `teardown` of the WebDriver / AppiumDriver sessions.
If you do not need "drivers" - e.g. you're writing some API tests, you should extend
`com.frameworkium.core.api.tests.BaseTest` instead.

For example:

```java
public class DynamicLoadingWebTest extends BaseTest { 
    //... 
}
```

## Look - no drivers!

As you can see in the example tests there are no references to WebDriver thanks to Frameworkium.
This results in more readable tests which only deal with the services offered by your application
and abstracts away the details and mechanics of it.
For further explanation see the [Page Objects](#_pages/Page-Objects.md) page.

```java
@Issue("BBA-5")
@Story("Logins")
@Test(description="Login to the application")
public void validLogin() {
    LandingPage.open().then()
            .clickLoginButton()
            .login("user", "password");
}
```

## Annotations

- `@Issue` is be used for JIRA & ZAPI reporting, JQL Query executions, and within the Allure report
- `@Story` utilise Allure's Features and Stories hierarchy and make larger test suites easier to manage
- `@Test` contains the description of the test, and can include a number of other details
-- *(`alwaysRun`, `dataProvider`, `dataProviderClass`, `dependsOnGroups`, `dependsOnMethods`, 
`description`, `enabled`, `expectedExceptions`, `groups`, `invocationCount`, `invocationTimeOut`, 
`invocationcounts`, `priority`, `successPercentage`, `singleThreaded`, `timeOut`, `threadPoolSize`)*
see [TestNG Annotations](http://testng.org/doc/documentation-main.html#annotations) for further details.
