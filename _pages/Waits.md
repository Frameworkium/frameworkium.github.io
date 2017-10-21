---
layout: post
title:  "Waits"
category: wiki
section: 4 - Page Object Guidance
order: 3
---

**Only use waits in your Page Object - _never_ in your tests**

You should not need to do many explicit waits - the `@Visible` tags etc. should handle the majority of cases.

However - there are times when you'll need to wait. For example:

 - we want to click a button
 - the button is initially hidden; but made visible by linking the 'more' arrow

So we want to click the 'more' arrow, then wait for the button to be visible before clicking on it.
We use `wait.until` and `ExpectedConditions`, as in the following example:

```java
@Visible
@Name("More Arrow")
@FindBy(css = "div#more-arrow")
private WebElement moreArrow;

@Name("Initially hidden button")
@FindBy(css = "div#button")
private WebElement initiallyHiddenButton;

public Page clickInitiallyHiddenButton() {
  moreArrow.click();
  wait.until(ExpectedConditions.visibilityOf(initiallyHiddenButton));
  initiallyHiddenButton.click();
  return this;
}
```

`ExpectedConditions` has lots of methods to help your waits - e.g.
`elementToBeSelected()`, `titleContains()`, `textToBePresentInElement()`, `textToBePresentInElementValue()`, etc. - see [here](https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/support/ui/ExpectedConditions.html) for the full list.

We have introduced our own extension to `ExpectedConditions` called `ExtraExpectedConditions`.

NB - Frameworkium has implicit waits due to our use of HtmlElements.
