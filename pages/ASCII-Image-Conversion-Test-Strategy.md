# Test Strategy - Image Conversion

### Automation
* In order to have concrete expected results, the conversion must first be validated manually. Across all image types and various dimensions.
    * See: Image Functional Tests for examples
    * Once a conversion result has been verified manually and signed off on by cross-functional team members,
        the text result can be saved as a expected result file that is checked in and used for comparison in automated tests.
        Example:
          Text input: "tempus_logo.png"
          Verified output:
                      "verified_converted_logo.svg"
          Text input: "image with text.jpg"
          Verified output:
                      "image with text converted with visible text.html"

    * The above output is saved as a file or in a variable to be read in at runtime
    * The input and expected result can be verified in automated tests continuously
    * There will be some legwork to initially set up the data, but the payoff will be immense for subsequent build verification
    * In this example, there are only a few preset options for font and input character types, so all comparisons can be built relatively easily
        * If more fonts or other inputs are introduced in the future, it may make sense to look at pairwise testing, to trim down the number of examples

### Manual Verification
  * Long-term, we don't want manual testing to be a trusted and necessary step for launching (and maintaining) this feature. Most functional aspects of the feature can reasonably be covered in automated tests.
  * There is a tremendous amount of value in exploratory testing pre-launch, as long as it as positioned as "cya" or "human eyes".
  * Exploratory testing can be focused on things like navigation (what happens if i use the browser back button, then forward?)
    * Obselete or old versions of browsers that a small number of users still use

### Monkey testing (and other miscellaneous)
  * use monkey testing to slam page with random inputs and checks for errors
  * See Non-functionals
  * Load
  * Security
