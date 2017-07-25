# Functional Testing - Image
* Automated tests should access a test version of the application, interact with the browser for inputs, and verify expected functionality.

```ruby
Given I am a visitor, I should see options to choose to convert my image to monochrome ASCII art or color ASCII art, and I can only choose one option. 
```

#### Validate Image Input (URL)
```ruby
Given I am a visitor, when I choose to convert a valid image by url, I should see the image transformed into ASCII art, as well as options to dowload as Text, HTML, or SVG.
```
| Test Identifier | URL Input | Assertion |
| --------- | ----- | --------- |
| Simple url | http://testimage.com | Success |
| Https | https://imgur.com/testimage | Success |

```ruby
Given I am a visitor, when I choose to convert an invalid image by url, I should be informed of my error and prompted to fix.
```
| Test Identifier | URL Input | Assertion |
| --------- | ----- | --------- |
| Invalid url | http://url with a space | Failure |
| Invalid url domain | http://test.x | Failure |
| Image too large | http://image>5M.jpg | Failure |
| Empty image | http://empty_image.png | Failure |
----
#### Validate Image Input (file extension)
```ruby
Given I am a visitor, when I choose to convert a valid uploaded image, I should see the image transformed into ASCII art, as well as options to dowload as Text, HTML, or SVG.
```
| Test Name | Image Input | Assertion |
| --------- | ----- | --------- |
| Simple png | file://simple.png | Success |
| Simple jpg | file://simple.jpg | Success |
| Simple jpeg | file://simple.jpeg | Success |
| Simple bmp | file://simple.bmp | Success |
| Simple gif | file://simple.gif | Success |

```ruby
Given I am a visitor, when I choose to convert an invalid uploaded image, I should see the image transformed into ASCII art, as well as options to dowload as Text, HTML, or SVG.
```
| Test Name | Image Input | Assertion |
| --------- | ----- | --------- |
| Invalid extension | file://bad.xz87fd | Failure |
| File too large | file://image>5M.png | Failure |
| Empty file | file://image_empty.jpg | Failure |
