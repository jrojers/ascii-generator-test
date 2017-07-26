# Functional Testing - Image
* Automated tests should access a test version of the application, interact with the browser for inputs, and verify expected functionality.

```ruby
Given I am a visitor
I should see options to choose to convert my image to monochrome ASCII art or color ASCII art
    And I can only choose one option
```
##### Example Test Implementation
NOTE: There are several options available to interact with the browser. Something like Capybara or PhantomJS allow you to interact with a simulated browser, without a "real" browser taking over a machine. Real browsers are slow and unstable over thousands of tests per day. In this example I chose basic Webdriver, which utilizes a real browser.

It is important to note that this example lives in the app repository, and would use the same test runner and reporting mechanisms that all unit (and other) tests use.

```ruby
describe 'ASCII Generator Image Conversion -' do  
  it "shows me options of Monochrome or Color ASCII art, and I can only choose one" do
    @driver.navigate.to "http://www.ascii-art-generator.org/"
  
    raise "Unable to load Generator." unless @driver.title.include? "Online ASCII Art Creator"

    # Verify available Image conversion options
    # Verify only one can be selected at a time
  end
end
```

----

#### Validate Image Input (URL)
```ruby
Given I am a visitor
When I choose to convert a valid image by url
I should see the image transformed into the chosen ASCII art
And be shown options to dowload as Text, HTML, or SVG
```

| Test Identifier | url | color | expected_results |
| --------- | ----- | ----- | --------- |
| Simple monochrome url png| http://testimage.png | monochrome | expected/simple_monochrome_png.txt, expected/simple_monochrome_png.svg, expected/simple_monochrome_png.svg |
| Simple color url png | http://testimage.png | color | expected/simple_color_png.txt, expected/simple_color_png.svg, expected/simple_color_png.svg |
| Https monochrome png | https://imgur.com/testimage.png | monochrome | expected/https_monochrome_png.txt, expected/https_monochrome_png.svg, expected/https_monochrome_png.svg |
| Https color png | https://imgur.com/testimage.png | color | expected/https_color_png.txt, expected/https_color_png.svg, expected/https_color_png.svg |

.
.
.
(and so on for all image file types **png, jpg, jpeg, bmp, gif**)


* TEST IMPLEMENTATION NOTES:
    * "Success" is defined as:
        1. Choose to convert "Image to Ascii"
        1. Provide image to convert (via url or upload)
        1. Verify option to download txt, html, svg files
        1. Download files and verify contents

```ruby

examples = { } #read in table of test inputs + expectations (see above)
           # example: [ {:url => "http://testimage.png", :color => 'monochrome', :expected_results => expected/simple_monochrome.txt, expected/simple_monochrome.svg, expected/simple_monochrome.svg} ]

describe 'ASCII Generator Image Conversion -' do
  it "can generate Monochrome ASCII art preview" do
    @driver.navigate.to "http://www.ascii-art-generator.org/"
  
    raise "Unable to load Generator." unless @driver.title.include? "Online ASCII Art Creator"
  
    examples.each do |ex|
      expected = IO.read(ex['expected_results'])
      (@driver.find_element :name, "art_type").select(1) # select Image to Monochrome Ascii Art Banner
      (@driver.find_element :name, "userfile_url").send_keys ex['url']
      (@driver.find_element :name, "submit").click()

      # Download files and compare size and contents to expected/simple_monochrome.txt, expected/simple_monochrome.svg, expected/simple_monochrome.svg
    end
  end
```


```ruby
Given I am a visitor
When I choose to convert an invalid image by url
I should be informed of my error and prompted to fix
```

| Test Identifier | url | Assertion |
| --------- | ----- | --------- |
| Invalid url | http://url with a space | Failure |
| Invalid url domain | http://test.x | Failure |
| Image too large | http://image>5M.jpg | Failure |
| Empty image | http://empty_image.png | Failure |
----

#### Validate Image Input (file extension)
```ruby
Given I am a visitor
When I choose to convert a valid uploaded image
I should see the image transformed into the chosen ASCII art
And be shown options to dowload as Text, HTML, or SVG
```

| Test Name | image_input | color | expected_results |
| --------- | ----- | ----- | --------- |
| Simple monochrome png | file://simple.png | monochrome | expected/simple_monochrome.txt, expected/simple_monochrome.svg, expected/simple_monochrome.svg |
| Simple color png | file://simple.png | color | expected/simple_color.txt, expected/simple_color.svg, expected/simple_color.svg |
| Simple monochrome jpg | file://simple.jpg | monochrome | expected/simple_monochrome.txt, expected/simple_monochrome.svg, expected/simple_monochrome.svg |
| Simple color jpg | file://simple.jpg | color | expected/simple_color.txt, expected/simple_color.svg, expected/simple_color.svg |

.
.
.
(and so on for all image file types **png, jpg, jpeg, bmp, gif**)

```ruby
Given I am a visitor
When I choose to convert an invalid uploaded image
I should see the image transformed into ASCII art
And shown options to dowload as Text, HTML, or SVG.
```
| Test Name | Image Input | Assertion |
| --------- | ----- | --------- |
| Invalid extension | file://bad.xz87fd | Failure |
| File too large | file://image>5M.png | Failure |
| Empty file | file://image_empty.jpg | Failure |
