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
        1. Enter text to convert
        1. Choose selected font
        1. Verify ASCII art preview matches provided input
        1. Verify option to download txt file
        1. Download file and verify contents

###### Example Test Implementation
NOTE: There are several options available to interact with the browser. Something like Capybara or PhantomJS allow you to interact with a simulated browser, without a "real" browser taking over a machine. Real browsers are slow and unstable for thousands of tests per day. In this example I chose Webdriver.

Important to note that this example lives in the app repository, and would use the same test runner and reporting mechanisms that all unit (and other) tests use.

```ruby

examples = { } #read in table of test inputs + expectations

describe 'ASCII Generator Text Conversion -' do
  it "can generate ASCII art preview" do
    @driver.navigate.to "http://www.ascii-art-generator.org/"
  
    raise "Unable to load Generator." unless @driver.title.include? "Online ASCII Art Creator"
  
    examples.each do |ex|
      (@driver.find_element :name, "art_type").select(3) # select Text to Ascii Art Banner
      (@driver.find_element :name, "banner_text").send_keys "HELLO"
      (@driver.find_element :name, "submit").click()

      banner_text = (@driver.find_element :id, "result-preview-wrap").getText()
      expect(banner_text).to eq(ex['expected_result'])
    end
  end
  
  it "can generate ASCII art in a file available for download" do
    @driver.navigate.to "http://www.ascii-art-generator.org/"
  
    raise "Unable to load Generator." unless @driver.title.include? "Online ASCII Art Creator"
  
    examples.each do |ex|
      (@driver.find_element :name, "art_type").select(3) # select Text to Ascii Art Banner
      (@driver.find_element :name, "banner_text").send_keys "HELLO"
      (@driver.find_element :name, "submit").click()
      
      # Download generated text file, assert contents
    end
  end

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

```ruby

describe 'ASCII Generator Text Conversion -' do
  it "does not generate ASCII art for empty text" do
    @driver.navigate.to "http://www.ascii-art-generator.org/"
  
    raise "Unable to load Generator." unless @driver.title.include? "Online ASCII Art Creator"
  
    (@driver.find_element :name, "art_type").select(3) # select Text to Ascii Art Banner
    (@driver.find_element :name, "banner_text").send_keys "HELLO"
    (@driver.find_element :name, "submit").click()

    # verify error and prompt to fix
  end
end
```
