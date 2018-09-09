---
layout: post
title:  "Page Objects"
category: wiki
section: 2 - Basics
order: 4
---

## Code Structure

### BasePage

Page objects must extend `com.frameworkium.core.ui.pages.BasePage<T>`.

Where `T` is the type of the page you are creating e.g. `LoginPage`.

### Elements (Fields)

Elements should be `private` and should only be used by this class.

#### Annotations

- `@Name` allows additional reporting and debugging information to be used later.
- `@Visible` Frameworkium will wait for the element to be displayed before returning the page.
- `@InVisible` Frameworkium will wait for the element to NOT be displayed before returning the page.
- `@FindBy` is a [Selenium annotation][find-by-docs].

### Actions (bottom)

All `public` methods on the page (the page's interface) should return either:

- a Page Object,
- built-in Java data types e.g. `String` or
- custom data types or
- nothing e.g. `void`

**Nothing** Frameworkium or Selenium specific e.g. `WebElement` should be returned.

#### Navigation

If an action on a page results in moving to a new page, then you can instantiate a new
Page Object in one of two ways:

- `return new NextPagePage().get();` or
- `return PageFactory.newInstance(NextPagePage.class);`

A common mistake is omitting the `.get()` in the first option which will result
in a null pointer exception when trying to use the page object.
This is because none of the fields (`WebElement`s) will be initialised.

See the `validLogin()` method below.

If performing an action on a page results in staying on the same page, then you can simply use
`return this;` e.g. the `invalidLogin()` method below.

#### Annotations

- `@Step` enables rich reporting of the steps being run.
`{0}` and `{1}` (in the example below) will be replaced in reports with the values passed into the method.

### Example

```java
public class LoginPage extends BasePage<LoginPage> {
    
    @Name("Username text field")
    @Visible
    @FindBy(css="input#inputEmail")
    private WebElement usernameField;
    
    @Name("Password text field")
    @FindBy(css="input#inputPassword")
    private WebElement passwordField;
    
    @Step("Enter credentials and return logged in homepage")
    public LoggedInHomepage validLogin(String username, String password) {
        login(username, password);
        return new LoggedInHomepage().get();
    }
    
    @Step("Enter credentials and expect to stay on the login screen")
    public LoginPage invalidLogin(String username, String password) {
        login(username, password);
        return this;
    }
    
    @Step("Enter username {0} and password {1} and click login")
    private void login(String username, String password) {
        usernameField.clear();
        usernameField.sendKeys(username);
    
        passwordField.clear();
        passwordField.sendKeys(password);
    
        loginButton.click();
    }
}
```

[find-by-docs]: https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/support/FindBy.html
