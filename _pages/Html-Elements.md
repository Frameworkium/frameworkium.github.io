---
layout: post
title:  "Specialised WebElements"
category: wiki
section: 4 - Page Object Guidance
order: 6
---
Page Objects use the `@FindBy` annotation and `PageFactory` to identify,
model and create elements on the web page. These are often `WebElement`s,
however, because Frameworkium uses the
[Yandex HtmlElements library](http://htmlelements.qatools.ru/)
we can make use of more specialised Objects.

## HtmlElements Examples

The most useful are the `CheckBox`, `Select`, `Radio`, `Form`, and `FileInput`.
Please read the documentation and explore their API in IntelliJ.

## Tables

There is also a `Table` which is suitable for small tables, however it is
not efficient and sometimes difficult to use.

### StreamTable

This is why we created `StreamTable`. It utilises two features from Java 8,
namely `Stream`s and `Optional`. If you are not familiar with these, please take
the time to learn as they will greatly improve the code you are able to write.

`Stream`s are lazy which means they will only do the minimum amount of work
required to you the task you set them. This is the largest benefit of 
`StreamTable`.

#### OptimisedStreamTable

`OptimisedStreamTable` is the same as `StreamTable` however it does not
check each element for `isDisplayed` therefore will not work as expected
on tables with hidden rows or columns.

`OptimisedStreamTable` is approximately twice as fast as `StreamTable`.

#### AbstractStreamTable

If none of the above Table Objects work for your application then you
can create your own Table `HtmlElement` by extending `AbstractStreamTable`.

You then have to implement three of the methods to specialise your new class
for your use case.
