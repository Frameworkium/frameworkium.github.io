---
layout: post
title: "A Couple of Cool Things"
section: 1 - What's The Point?
order: 3
category: wiki
---
To whet the appetite,
here's a couple of examples where Frameworkium features make your life easier.

## @Visible

Say you're expecting an element on a web page, and you want to wait until
it's there and visible before clicking on it.

### Vanilla Selenium

```java
WebElement button = driver.findElement(By.cssSelector("#search_button");
WebDriverWait wait = new WebDriverWait(driver, 10);
wait.until(ExpectedConditions.visibilityOf(button));
button.click();
```

You could probably do this with a (longish) one-liner,
but if we were trying to make the code nice and maintainable etc.

### PageFactory

```java
// at the top of your class
@FindBy(css="#search_button")
private WebElement button;

// when you want to use it
WebDriverWait wait = new WebDriverWait(driver, 10);
wait.until(ExpectedConditions.visibilityOf(button));
button.click();
```

Which is nicer, because:

1. The CSS selector for a control is in *one* place, rather than repeating it every time you use it.
It changes? You update the 1 instance, rather than 5+.

2. `PageFactory` removes the need for quite so much `driver.` action - again reducing the reuse, overlap, repetition, etc

*(NB If you've never heard of [PageFactory](https://github.com/SeleniumHQ/selenium/wiki/PageFactory),
it's a pattern for using page objects that's part of the selenium libraries)*

#### Frameworkium then builds on this:

```java
// at the top of your class
@Visible
@FindBy(css="#search_button")
private WebElement button;

// when you want to use it
button.click();
```

By using the `@Visible` annotation, when the page loads you'd automatically wait
for the button to be visible. Which further neatens things - particularly when 
you imagine there might be 10-20 things on a page that we _might_ want to wait for.

There's also an `@Invisible`, and both works with `List<WebElement>`, `HtmlElement`s etc.
