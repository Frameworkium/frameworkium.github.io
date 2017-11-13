---
layout: post
title:  "JavaScript Hacks"
category: wiki
section: "7 - Other"
order: 8
---

## Warning

Do **NOT** use these unless it's the last remaining option.

Your tests are supposed to be simulating user actions and user flows, so injecting JavaScript is 
_not_ to be used unless some weirdness means that selenium cannot do something that a user can.

## Example: Un-Hiding Hidden Controls

In order to upload a file to a site, the 'choose files' input control is used.
See [Native Controls][native] for how we handle this scenario using the `SendKeys` directly to input controls.

### Problem

In some cases, the input control might be hidden on the page, with a `div` on top of it:

```html
<div id="input-button">
  <input class="hidden" />
</div>
```

SendKeys to the `div` will not have the same effect as SendKeys to the `input`,
and because the input control is hidden, Selenium cannot interact with it.

### Solution

We've have added the `@ForceVisible` annotation for this scenario.

```java
@ForceVisible
@Name("Upload input")
@FindBy(css="div#upload-button input")
private WebElement uploadInput;

@Step("Upload a file")
public void tryAnUpload(File fileToUpload) {
  //Send the file path directly to the input button via sendKeys
  uploadInput.sendKeys(fileToUpload.getAbsolutePath());
}
```

On page load, Frameworkium will try to un-hide the control with JavaScript.
If you'd like to control when it happens, use
`this.visibility.forceVisible(uploadInput)` instead of `@ForceVisible`.

### Old Solution

The old solution was to use a JavaScript executor in your page object to modify the style of the
input such that selenium can interact with it.

The method below demonstrates this.

```java
@Name("Upload input")
@FindBy(css="div#upload-button input")
private WebElement uploadInput;

@Step("Upload a file")
public void tryAnUpload(File fileToUpload) {
  // CSS Locator for the hidden input button
  String cssSelector = "div#upload-button input";

  // Use JavaScript executor to make the input button visible
  // 'super' as it's using a method on the superclass (BasePage)
  super.executeJS("document.querySelector('" + cssSelector + "').style.width = '200px'");
  super.executeJS("document.querySelector('" + cssSelector + "').style.height = '10px'");
  super.executeJS("document.querySelector('" + cssSelector + "').style.opacity = '100'");

  // Send the file path directly to the input button via sendKeys
  uploadInput.sendKeys(fileToUpload.getAbsolutePath());
}
```

This sort of idea can also be used if you need to do more than `@ForceVisible` or would like to
have more control over what happens, it's just a bit more verbose.

## Trade Offs

UI automation testing is largely about simulating user's behaviour as best we can.
We could use some other tool (e.g. autoIt, Sikuli, call the JavaScript function directly etc.),
but the additional flakiness and complexity this introduces will likely outweigh the benefit.

It's about choosing the simplest and most reliable approach to get the job done.

[native]: /#_pages/Native-Controls.md
