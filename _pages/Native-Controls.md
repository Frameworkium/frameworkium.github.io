---
layout: post
title:  "Native Controls"
category: wiki
section: 6 - Advanced Usage
order: 7
---

## Alerts/Dialog boxes

[This test](https://github.com/Frameworkium/frameworkium-examples/blob/master/src/test/java/com/heroku/theinternet/tests/web/TheInternetExampleTests.java#233) demonstrates the use of the `switchTo().alert()` functionality that selenium uses to interact with javascript alert popups.
The page object [here](https://github.com/Frameworkium/frameworkium-examples/blob/master/src/test/java/com/heroku/theinternet/pages/web/JavaScriptAlertsPage.java) contains the methods that accept, dismiss, cancel, ok, and enter text to a variety of different native JS popups.
These are summarised below:

```java
// To accept an alert (e.g. click 'yes' or 'accept' or 'ok'
driver.switchTo().alert().accept();

// To dismiss or cancel an alert (e.g. click 'no' or 'dismiss' or 'cancel')
driver.switchTo().alert().dismiss();

// To enter text on an alert requiring text entry
driver.switchTo().alert().sendKeys(textToEnter);

// To enter authentication on an alert requiring a username & password
Credentials credentials = new UsernamePasswordCredentials("username", "password");
driver.switchTo().alert().authenticationWith(credentials);
```

## Handling file pickers - e.g. 'Choose Files' button

In order to upload a file to a site, the 'choose files' input control is used.
To a user, this will open a file browser on whatever platform they're on.
Selenium cannot interact with this native control.

In order to get around this, we can SendKeys(/path/to/file) directly on the
input control - e.g. `chooseFilesInputButton.sendKeys("/path/to/file");`,
which bypasses the file browser that selenium cannot handle.

The example below demonstrates how to perform this on the 
[Heroku File Upload](http://the-internet.herokuapp.com/upload) page.
The full example page object can be seen 
[here](https://github.com/Frameworkium/frameworkium-examples/blob/master/src/test/java/com/heroku/theinternet/pages/web/FileUploadPage.java) and the test that uses this [here](https://github.com/Frameworkium/frameworkium-examples/blob/master/src/test/java/com/heroku/theinternet/tests/web/TheInternetExampleTests.java#L140)

```java
@Visible
@Name("Choose Files button")
@FindBy(css = "input#file-upload")
private WebElement chooseFilesButton;

@Visible
@Name("Upload button")
@FindBy(css = "input#file-submit")
private WebElement uploadButton;

@Step("Upload a file by choosing file and then clicking upload")
public FileUploadSuccessPage uploadFile(File filename) {
  chooseFilesButton.sendKeys(filename.getAbsolutePath());
  uploadButton.click();
  return PageFactory.newInstance(FileUploadSuccessPage.class);
}
```

### Why not use AutoIt, Sikuli etc.

Running locally, on your machine, with your config etc., a number of solutions may work perfectly well.
However, the main problems come when you want to ramp things up - what about:
- running tests in parallel?
- other browsers - does it behave the same?
- other OSs - mac dialogs are very different to windows etc.
- on a grid - more dependencies required (e.g. AutoIt must be present on all your grid nodes)
- reliability

We want to try and keep our test pack as scalable and multi-platform as possible - 
although we're bypassing the OS's file browser by sending keys directly to the input control here.
It's important to remember our main focus is testing _our application_ - not the browser's file picker functionality.
