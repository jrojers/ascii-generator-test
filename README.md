# ASCII Art Generator Test Plan

## Table of Contents
1. [Build Quality In](./pages/ASCII-Build-Quality-In.md)
2. [Testing Methodology](./pages/ASCII-Methodology.md)
3. Test Strategies
    * [Text Conversion](./pages/ASCII-Text-Conversion-Test-Strategy.md)
    * [Image Conversion](./pages/ASCII-Image-Conversion-Test-Strategy.md)
3. Functional Testing
    * [Text => ASCII Art](./pages/ASCII-Generator-Testing-Text.md)
    * [Image => ASCII Art](./pages/ASCII-Generator-Testing-Image.md)
4. [Non-functional Testing](./pages/ASCII-Generator-Nonfunctionals.md)

## Assumptions
    a. The ASCII Art Generator lives in one primary code repository.

## Directives
* Automated tests and infrastructure are important and sensitive. All changes must be reviewed and merged following existing protocols.
* Unit, Functional, and Performance tests live in the same repository with the functions they are testing. (See Assumption A above.) 
* All automated tests run with the same test runner and infrastructure that already exists for unit tests. (ie. Rspec, Mocha, Karma, JUnit, etc.)
* All automated tests run in continuous integration (ie. Jenkins, CircleCI, Bamboo, etc.)
