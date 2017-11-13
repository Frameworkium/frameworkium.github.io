---
layout: post
title:  "Allure Reporting"
category: wiki
section: 5 - Logging & Reporting
order: 7
---

You can generate an [Allure][allure] test report by running:

```bash
mvn site
```

Then, open `target/site/allure-maven-plugin.html` to view the report.

_NB Either open via IntelliJ (they host it on a local web server for you) or use another browser!_

This will interpret `@Step`, `@Issue`, `@Features` and `@Story` annotations,
and provide rich reporting on the suite just run.

## Jenkins

When running tests via Jenkins, the [Allure Jenkins Plugin][allure-jenkins-plugin] can be added to
the Jenkins job, and it will automatically produce and store reports for every run.

[allure]: http://allure.qatools.ru/
[allure-jenkins-plugin]: https://wiki.jenkins.io/display/JENKINS/Allure+Plugin
