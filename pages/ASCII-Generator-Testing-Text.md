# Functional Testing
* Automated tests should access a test version of the application, interact with the browser for inputs, and verify expected functionality.

#### Validate Text Input
```ruby
Given I am a visitor
When I provide valid text to the generator
Then I should see my text transformed into ASCII text in the font I choose, 
      with the ability to download the result as text
```
| Test Identifier | Text Input | Font | Assertion |
| --------- | ----- | ----- | --------- |
| Simple Text Banner | HELLO | banner | Success |
| Numbers Banner | 12234 | banner |Success |
| Mixed Banner | 123halkdjhf13123adfjha | banner |Success |
| Special characters Banner | 123*(*akjfd*(& | banner |Success |
| Small characters Banner | ....... | banner | Success |
| Simple Text Big | HELLO | big | Success |
| Numbers Big | 12234 | big |Success |
| Mixed Big | 123halkdjhf13123adfjha | big |Success |
| Special characters Big | 123*(*akjfd*(& | big |Success |
| Small characters Big | ....... | big | Success |
| Simple Text Block | HELLO | block | Success |
| Numbers Block | 12234 | block |Success |
| Mixed Block | 123halkdjhf13123adfjha | block |Success |
| Special characters Block | 123*(*akjfd*(& | block |Success |
| Small characters Block | ....... | block | Success |

.
.
.
(and so on for all fonts **banner, big, block, bubble, lean, mini, script, shadow, slant, standard]**)

* TEST IMPLEMENTATION NOTES:
    * "Success" is defined as:
        1. Choose to convert "Text to Ascii"
        2. Enter text
        3. Choose selected font
        4. Verify ASCII art preview exists
        5. Verify text in input is legible in ASCII art
        5. Verify option to download txt file
        6. Download file and verify size and contents

###### Example Test Implementation
```ruby
describe 'ASCII Generator Text Conversion -' do
  it 'should convert text with chosen font to ASCII art' do
    page.load('http://www.ascii-art-generator.org/')
    page.findElement(driver.By.name("banner_text")).sendKeys("HELLO");
  end
```

----
```ruby
Given I am a visitor
When I provide invalid text to the generator
Then I should be informed that I provided invalid input, and to try again. 
```
| Test Identifier | Input | Assertion |
| --------- | ----- | --------- |
| Empty Text | | Error |
| Too many chars | {Max # characters} | Error |
