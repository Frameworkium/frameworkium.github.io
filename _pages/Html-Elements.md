---
layout: post
title:  "HTMLElements"
category: wiki
section: 4 - Page Object Guidance
order: 6
---
Page Objects use the `@FindBy` annotation and `PageFactory` to identify and
model elements on the web page. These can simply be `WebElement`s, however 
Frameworkium uses the [Yandex HtmlElements library](http://htmlelements.qatools.ru/) 
which means we can make use of more specialised Objects.

## HtmlElements Examples

The most useful are the `CheckBox`, `Select`, `Radio`, `Form`, and `FileInput`.

## Tables

There is also a `Table` which is suitable for small tables, however it is highly
inefficient and sometimes difficult to use.

### StreamTable

This is why we created `StreamTable`. It utilises two features from Java 8,
namely `Stream`s and `Optional`. If you are not familiar with these, please take
the time to learn as they will greatly improve the code you are able to write.

`Stream`s are lazy which means they will only do the minimum amount of work
required to you the task you set them. This is the largest benefit of `StreamTable`. 