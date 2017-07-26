# Functional Testing - Text Conversion
* Automated tests should access a test version of the application, interact with the browser for inputs, and verify expected functionality.

#### Validate Text Input
```ruby
Given I am a visitor
When I provide valid text to the generator
Then I should see my text transformed into ASCII text in the font I choose, 
      with the ability to download the result as text
```
| Test Identifier | text_input | Font | expected_result |
| --------- | ----- | ----- | --------- |
| Simple Text Banner | HELLO | banner | [expected/hello_banner.txt](../expected/hello_banner.txt) |
| Numbers Banner | 12234 | banner | expected/numbers_banner.txt |
| Mixed Banner | 123halkdjhf13123adfjha | banner | expected/mixed_banner.txt |
| Special characters Banner | 123*(*akjfd(& | banner | expected/special_banner.txt |
| Small characters Banner | ....... | banner | expected/small_banner.txt |
| Simple Text Big | HELLO | big | expected/simple_big.txt |
| Numbers Big | 12234 | big | expected/numbers_big.txt |
| Mixed Big | 123halkdjhf13123adfjha | big | expected/mixed_big.txt |
| Special characters Big | 123*(*akjfd(& | big | expected/special_big.txt |
| Small characters Big | ....... | big | expected/small_big.txt |
| Simple Text Block | HELLO | block | expected/simple_block.txt |
| Numbers Block | 12234 | block | expected/numbers_block.txt |
| Mixed Block | 123halkdjhf13123adfjha | block | expected/mixed_block.txt |
| Special characters Block | 123*(*akjfd(& | block | expected/special_block.txt |
| Small characters Block | ....... | block | expected/small_block.txt |

.
.
.
(and so on for all fonts **banner, big, block, bubble, lean, mini, script, shadow, slant, standard**)

* TEST IMPLEMENTATION NOTES:
    * "Success" is defined as:
        1. Choose to convert "Text to Ascii"
        1. Enter text to convert
        1. Choose selected font
        1. Verify ASCII art preview matches provided input
        1. Verify option to download txt file
        1. Download file and verify contents

##### Example Test Implementation
NOTE: There are several options available to interact with the browser. Something like Capybara or PhantomJS allow you to interact with a simulated browser, without a "real" browser taking over a machine. Real browsers are slow and unstable over thousands of tests per day. In this example I chose basic Webdriver, which utilizes a real browser.

It is important to note that this example lives in the app repository, and would use the same test runner and reporting mechanisms that all unit (and other) tests use.

```ruby

examples = { } #read in table of test inputs + expectations (see above)
           # example: [ {:text_input => "HELLO", :expected_result => hello_banner.txt} ]

describe 'ASCII Generator Text Conversion -' do
  it "can generate ASCII art preview" do
    @driver.navigate.to "http://www.ascii-art-generator.org/"
  
    raise "Unable to load Generator." unless @driver.title.include? "Online ASCII Art Creator"
  
    examples.each do |ex|
      expected = IO.read(ex['expected_result'])
      (@driver.find_element :name, "art_type").select(3) # select Text to Ascii Art Banner
      (@driver.find_element :name, "banner_text").send_keys ex['text_input']
      (@driver.find_element :name, "submit").click()

      banner_text = (@driver.find_element :id, "result-preview-wrap").getText()
      expect(banner_text).to eq(expected)
    end
  end
  
  it "can generate ASCII art in a file available for download" do
    @driver.navigate.to "http://www.ascii-art-generator.org/"
  
    raise "Unable to load Generator." unless @driver.title.include? "Online ASCII Art Creator"
  
    examples.each do |ex|
      (@driver.find_element :name, "art_type").select(3) # select Text to Ascii Art Banner
      (@driver.find_element :name, "banner_text").send_keys ex['text_input']
      (@driver.find_element :name, "submit").click()
      
      # Download generated text file, assert contents
      expect(file).to eq(ex['expected_result'])
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
