# Test Strategy - Image Conversion

### Automation
* In order to have concrete expected results, the conversion must first be validated manually. Across all image types and various dimensions.
    * See: [Image Conversion Examples](../pages/ASCII-Generator-Testing-Image.md).
    * Once a conversion result has been verified manually and signed off on by cross-functional team members, the generated result can be saved as a expected result file that is checked in and used for comparison in automated tests.
        * Example:
          * Image input: 
            - ![alt text](../images/tempus.jpg)
          * Verified output:
            - ![alt text](../images/tempus.png)
        * Example:
          * Text input: "image with text.jpg"
          * Verified output:
    * The above output is saved as a file to be read in at runtime.
    * The input and expected result can be verified in automated tests continuously.
    * There will be some legwork to initially set up the expected data, but the payoff will be immense for subsequent build verification.
    * In this example, there are only a few options for urls, uploaded images, and file types, so all comparisons can be built relatively easily.

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
  * Hold onto image for 20+ minutes
