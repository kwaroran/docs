# HTML in RisuAI

RisuAI supports inserting HTML tags (like `<b>`, `<i>`, `<a>`, etc.) in the text. This is useful for formatting the text in a more advanced way.

Example:
```html
<b>This is bold text</b>
<i>This is italic text</i>
<img src="{{raw::aa}}"> <!-- This is an image -->
```

Some tags and attributes are treated specially:
- `<style>`: The css inside this tag would be trimmed down to a safe subset of css properties and values. and class names would be renamed to prevent conflicts.
- `<iframe>`: If is a youtube video, it would be embedded in the chat. Otherwise, it would be removed.
- `class` attribute: The class names would be renamed to prevent conflicts. since the css's class names are renamed, the class names in the HTML tags would still work.
- `href` attribute: The attribute would be removed if it is not a valid URL.
- `translate` attribute: If the attribute is set to `no`, the element won't be translated.
- `risu-trigger` attribute: If the attribute is set, if the user clicks on the element, the trigger named in the attribute would be triggered.

RisuAI also adds some new XML tags:
- `<Comment>`: This tag is used to insert comments in the text. The text inside this tag would be hidden for both the user and the AI.
- `<Thoughts>`: This tag is used to insert thoughts of AI in the text. The text inside would be hidden for the user but would be used by the AI to generate the response.


the HTML tags are trimed down to a safe subset of tags and attributes to prevent XSS attacks. 


