# Markdown

On Risuai, you can use Markdown to format your text. Markdown is a easy-to-read and easy-to-write syntax for styling text. We follow the CommonMark specification for Markdown.

## Supported

| Element | Syntax | Output |
| ----------- | ----------- | ----------- |
| Bold | `**bold text**` | **bold text** |
| Italic | `*italic text*` | *italic text* |
| Strikethrough | `~~strikethrough text~~` | ~~strikethrough text~~ |
| Ordered List | `1. First item`<br>`2. Second item` | 1. First item<br>2. Second item |
| Unordered List | `- First item`<br>`- Second item` | - First item<br>- Second item |
| Code | `` `code` `` | `code` |
| Link | `[text](url)` | [text](/syntax/markdown.md) |
| Horizontal Rule | `---` | (Not displayed on Docs) |
| Heading | `# Heading 1`<br>`## Heading 2`<br>`### Heading 3` | (Not displayed on Docs) |
| Table | `| Header 1 | Header 2 |`<br>`| ----------- | ----------- |`<br>`| Element 1 | Element 2 |` | (Not displayed on Docs) |

### Advanced Tips

- You can use HTML in Markdown. However, some tags and attributes are treated specially:
    - `<style>`: The css inside this tag would be trimmed down to a safe subset of css properties and values. and class names would be renamed to prevent conflicts.
    - `<iframe>`: If is a youtube video, it would be embedded in the chat. Otherwise, it would be removed.
    - `class` attribute: The class names would be renamed to prevent conflicts. since the css's class names are renamed, the class names in the HTML tags would still work.
    - `href` attribute: The attribute would be removed if it is not a valid URL.
    - `translate` attribute: If the attribute is set to `no`, the element won't be translated.
    - `risu-trigger` attribute: If the attribute is set, if the user clicks on the element, the trigger named in the attribute would be triggered.
- Formatting is disabled right after HTML tags. You need to add a new line after the tag to enable formatting.
- Backslashes are used to escape Markdown syntax. for example, `\~\~hello\~\~` will be displayed as `~~hello~~`, instead of strikethrough text ~~hello~~
- `_` can be used instead of `*` for italic text, and `__` can be used instead of `**` for bold text.
- Bold and Italic text can be combined. For example, `***bold and italic text***` will be displayed as ***bold and italic text***.
- `![foo](/url "title")` can be used to add images. however, We recommend using the `{{image::assetId}}` syntax to add images instead.
- URLs linking isn't supported due to security reasons.