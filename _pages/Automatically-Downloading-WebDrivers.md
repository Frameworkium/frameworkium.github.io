---
layout: post
title:  "Automatically Downloading WebDrivers"
category: wiki
section: "7 - Other"
order: 16
---

Since: `2.4.4`
Removed: `3.0.0`

Frameworkium supports the [driver-binary-downloader][plugin] Maven plugin,
which allows the automatic download of webdriver binaries from the Internet i.e.:

```bash
mvn driver-binary-downloader:selenium
```

The default parameters store the latest 64-bit drivers for the current OS under 
the `drivers/bin/` directory.
The configuration options can be parameterised to select specific versions,
different operating systems etc.
If all requested drivers are already present under the designated directory,
then no further actions take place at the back of this goal. 

For further information, visit the plugin's [GitHub page][plugin].

[plugin]: https://github.com/Ardesco/selenium-standalone-server-plugin
