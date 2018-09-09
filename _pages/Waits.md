---
layout: post
title:  "Waits"
category: wiki
section: 4 - Page Object Guidance
order: 3
---

Only use waits in your **Page Object** - _never_ in your tests

You should not need to do many explicit waits - the `@Visible` and `@Invisible`
tags etc., which work on Page Object load, should handle the majority of cases.

However - there are times when you'll need to wait. For example:

 - we want to click a button, but
 - the button is initially hidden; but made visible by linking the 'more' arrow

First we click the 'more' arrow, then wait for the button to be visible.
We can use `wait.until` and `ExpectedConditions`, as in the following example:

```java
public class MyPage extends BasePage<MyPage> {
    
    @Visible
    @FindBy(id = "more-arrow")
    private WebElement moreArrow;
    
    // Initially hidden button
    @FindBy(css = "div#button")
    private WebElement myButton;
    
    public Page clickInitiallyHiddenButton() {
      moreArrow.click();
      wait.until(ExpectedConditions.visibilityOf(myButton));
      myButton.click();
      return this;
    }
}
```

[ExpectedConditions][EC] has lots of methods to help your waits - e.g.
`elementToBeSelected(...)`, `titleContains(...)`, `textToBePresentInElement(...)`, 
`textToBePresentInElementValue(...)`, etc.

Frameworkium has it's own extension to `ExpectedConditions`,
called [`ExtraExpectedConditions`][EEC].

NB - Frameworkium (pre v3.0) has implicit waits due to our use of HtmlElements.

[EC]: https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/support/ui/ExpectedConditions.html
[EEC]: https://github.com/Frameworkium/frameworkium-core/tree/master/src/main/java/com/frameworkium/core/ui/ExtraExpectedConditions.java
