---
layout: post
title:  "Contibuting"
category: wiki
section: "8 - Contributing"
order: 16
---
To Contribute:
- Implement the feature on a branch
- When all tests are passing, submit a pull request
- Coding standards, based on the [Google Style Guide](https://github.com/google/styleguide) are enforced using Checkstyle. Formatters for Eclipse and IntelliJ are provided in the doc/style folder. Generic information on how to set up styles on Eclipse and Intellij can be found [here](https://github.com/HPI-Information-Systems/Metanome/wiki/Installing-the-google-styleguide-settings-in-intellij-and-eclipse).

To set up checkstyle in IntelliJ to parse the source code for style-related issues:
- Install Checkstyle-IDEA plugin into IntelliJ
- Locate the style XMLs in docs/style/
- Navigate to: Settings -> Other settings -> Checkstyle -> Press the green '+' symbol and add docs/style/style.xml -> Check Checkbox to activate it
- Navigate to: Settings -> Editor -> Inspections -> Click settings wheel button -> Import Scheme -> IntelliJ IDEA code style XML (try other options if it''s not there like the Eclipse one) -> intellij-java-style.xml -> add docs/style/intellij-java-style.xml
- You should now be able to use the intellij checkstyle plugin to run checkstyle scans over a class for the entire project