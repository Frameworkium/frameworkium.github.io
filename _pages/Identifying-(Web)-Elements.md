---
layout: post
title:  "Identifying Web Elements"
category: wiki
section: 4 - Page Object Guidance
order: 5
---
We identify elements on web pages using the `@FindBy` annotation, and passing in selector strings.

Try to pick selectors that are:

* human readable 
* least likely to change
* uniquely identify the element(s) you wish to interact with

### @FindBy(id = "fromButton")

ID's are the preferred way to find elements on a page. This is because they are
fast and (should be) unique and often human readable.

### @FindBy(css = "input#fromButton")

CSS selectors. These are the preferred means of identifying controls after ID.
CSS selectors are generally easier to read than xpath, and generally as fast or faster than xpath.
See [here](https://flukeout.github.io) for an interactive game to help you learn the syntax.

Developer tools for Firefox and Chrome allow you to identify and test your
CSS selectors before you put them into your pages.

### @FindBy(linkText = "Click here to view")

`linkText` does exactly what it says on the tin - searches for any links on the
page that display the text specified. _BEWARE_ - often the same text will be used 
in multiple places on a page, so use this with caution.

### @FindBy(xpath = "//div")

`xpath` selectors. Best avoided unless everyone on your team knows xpath well.
It's probably better to learn CSS selectors.
Xpath can be useful if you need to identify an element based on text _within_ 
an element, as you can specify "contains":

e.g.: `//div[contains(.,'Click here')]` will select the div `<div>Click here</div>`

Dev tools in the browsers allow you to test your selector before putting it into your code.

### Tips

* Try to select the actual element that you want to perform the operation on.e.g.
`<div id="link-button"><a href="blah">Link</a></div>` -> `css="#link-button a"`
will be more robust to _click_ than `css="div#link-button"` since it's actually the 
ink that you want - e.g. some browsers will treat the entire div as the link, others may not.

* **Element Visibility** -  Selenium will not find hidden controls on the page.
This is on purpose, since it's trying to simulate the activities of a real user.
However, if it's the ONLY way, you can use JavaScript injection to 'unhide' controls (see `@ForceVisible`).

* **Auto-Generated tags** - the naming conventions of buttons will entirely depend on the framework used.
Avoid using auto-generated 'id' tags, for example, as these tend to get regenerated when new pages/controls are added.
