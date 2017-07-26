# Non-functional Testing

Non-functional tests should be automated wherever possible, and should fail the build when the results are trusted.

### Examples
   1. [XSS testing](https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet) - The ASCII Art Generator includes text fields for the text to be converted, as well as an image URL field. Inputs are vulnerable to XSS attacks.
   2. Assuming there is a back-end that is processing the inputs for the ASCII art generator, it is possible to send an invalid request directly to the server (avoiding front-end validations). See: [Fiddler](http://www.telerik.com/fiddler).
   3. Performance. As touched on in the [Testing Methodology](./pages/Testing-Methodology.md), the performance of key functions need to be measured and graphed over time. Our functional tests should throw a measurement to a stats collector on every build execution. If a new commit causes the ASCII text generation to triple in processing time, we need to be aware of it.
   4. Load. We need to verify that the system can handle multiple connections, and handle multiple conversions (text & image) with concurrent threads.

### Miscellaneous
  * [Monkey Testing](https://monkeytest.it/). Slam the ASCII generator with random inputs and clicks, and verify that it responds as expected.
  * Timing. Generate a conversion (both text & image), then wait 20+ minutes. Try to download the generated txt file (or html/svg). The system should inform that it only holds onto images for 20 minutes.
     - A test like this can be automated by manipulating the system time settings. 

