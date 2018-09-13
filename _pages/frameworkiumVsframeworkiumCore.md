---
layout: post
title: "Examples vs. Core"
section: 1 - What's The Point?
order: 2
category: wiki
---
[`frameworkium-examples`][examples] is the example ("quick-start") project, 
designed for test engineers to download and use as an example for their own tests.
It comes with example tests for both web automation and REST APIs, which should
give an idea of how to structure new tests.

`frameworkium-core`][core] is a separate project, which contains (and tucks away)
all of the code that helps to simplify and keep tidy your tests.
You do **not** need to clone/edit/touch it - unless you want to help improve it by submitting a pull request!

It's updated [pretty frequently][core-releases];
to update your project to use the latest simply find and update the lines in your `pom.xml` file:

```xml
<dependency>
  <groupId>com.github.frameworkium</groupId>
  <artifactId>frameworkium-core</artifactId>
  <version>2.7.2</version>
</dependency>
```

Update the version number to the latest on the [releases][core-releases] page,
and _voila_ - you'll get the latest jars and dependencies (that have already been tested to work together).
Please make sure you read the [release notes][core-releases] to make sure none of the changes may break your existing tests.

[examples]: https://github.com/Frameworkium/frameworkium-examples
[core]: https://github.com/Frameworkium/frameworkium-core
[core-releases]: https://github.com/Frameworkium/frameworkium-core/releases
