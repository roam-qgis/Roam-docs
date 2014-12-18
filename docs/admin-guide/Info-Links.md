Roam will try to automatically handle URLs to websites and files in the info panel.  It will also try and display a file based, base64, or binary image.  If all else fails it will just display the string value.

**Link format** 

Links to websites should start wtih `http://` and links to files should start with `file:///`. Roam will check for both these and try to create a valid URL.

**Replace URL with alias**

The full URL can be aliased by appending `|alias` to the end of the URL string.  Example `http://google.com|Google` will just display as `Google` as a hyperlink in the info panel.
