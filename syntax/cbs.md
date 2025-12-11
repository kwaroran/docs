# Curly Braced Syntaxes

Curly braced syntaxes (like `{{user}}`) are used to insert special values into the text.
The syntaxes can be used in almost any text field in the client, including chat messages, character descriptions, and lorebook entries.

The syntaxes are replaced with the actual values when the message is sent or when the text is displayed in the client.
The syntaxes can be nested and combined with other syntaxes, for example:

```text
{{calc::{{getvar::a}}+{{getvar::b}}}}
```

!!!info Quick Reference
- **Case-insensitive**: `{{user}}`, `{{User}}`, and `{{USER}}` are all the same.
- **Parameters**: Separated by `::` (two colons), e.g., `{{getvar::myVar}}`
- **Arrays**: Use `{{array::A::B::C...}}` syntax to create an array.
- **Block syntaxes**: Start with `{{#NAME A}}` and end with `{{/NAME}}` or `{{/}}`. Content indentation is trimmed unless using `-pure` variants.
!!!

---

## Data Syntaxes [!badge variant="primary" text="Basic"]

+++ Character & User
### `{{user}}`

This will be replaced with the persona's name.

### `{{char}}`

This will be replaced with the character's name.

!!!secondary Note
In group chat: if the speaker is user, this will be replaced with group chat name. If the speaker is character, this will be replaced with the speaker's name.
!!!

### `{{description}}`

!!!ghost Alias
`{{char_desc}}`
!!!

This will be replaced with the character's description.

### `{{example_dialogue}}`

!!!ghost Alias
`{{example_message}}`
!!!

This will be replaced with an array of example dialogue of the character.

### `{{persona}}`

!!!ghost Alias
`{{user_persona}}`
!!!

This will be replaced with the persona's description.

+++ History & Lorebook
### `{{lorebook}}`

!!!ghost Alias
`{{world_info}}`
!!!

This will be replaced with array of lorebook entries.

### `{{history}}`

!!!ghost Alias
`{{messages}}`
!!!

This will be replaced with array of messages in current chat.

### `{{user_history}}`

This will be replaced with the array of messages of the user in the chat log.

### `{{char_history}}`

This will be replaced with the array of messages of the character in the chat log.

+++ Message Info
### `{{chat_index}}`

This will be replaced with the index of the message in the chat.

!!!warning Index Values
- Normal messages: start from `0`
- First message: has an index of `-1`
- Non-chat context: replaced with `-1`
!!!

### `{{lastmessage}}`

This will be replaced with the last message in the chat log.

### `{{lastmessageid}}`

!!!ghost Alias
`{{lastmessageindex}}`
!!!

This will be replaced with the index of the last message in the chat log.

### `{{previous_char_chat}}`

!!!ghost Alias
`{{lastcharmessage}}`
!!!

This will be replaced with the last message of the current character in the chat log.

### `{{previous_user_chat}}`

!!!ghost Alias
`{{lastusermessage}}`
!!!

This will be replaced with the last message of the user in the chat log.

### `{{previous_chat_log::A}}`

This will be replaced with the chat message with the index of `A` in the chat log. If the message does not exist, it will be replaced with `Out of range`

### `{{first_msg_index}}`

This will be replaced with the index of the first message in the chat log.

+++ Model & System
### `{{model}}`

This will be replaced with the current model id of the client.

### `{{axmodel}}`

This will be replaced with the current auxiliary model id of the client.

### `{{role}}`

This will be replaced with the current role of the message sender.
If the `{{role}}` is used in non-chat context, it will be replaced with `role` string.

### `{{maxprompt}}`

This will be replaced with the maximum tokens setting of the client.

### `{{screen_width}}`

This will be replaced with the width of the screen in pixels.

### `{{screen_height}}`

This will be replaced with the height of the screen in pixels.
+++

---

## Time Syntaxes [!badge variant="info" text="Time"]

+++ Basic Time
### `{{time}}`

This will be replaced with the current time, in the format `HH:MM:SS` in client's timezone.

### `{{date}}`

This will be replaced with the current date, in the format `YYYY-MM-DD` in client's timezone.

### `{{isotime}}`

This will be replaced with the current time, in the format `HH:MM:SS` in the UTC timezone.

### `{{isodate}}`

This will be replaced with the current date, in the format `YYYY-MM-DD` in the UTC timezone.

+++ Formatted Time
### `{{time::A}}`

!!!ghost Alias
`{{datetimeformat:A}}`, `{{date::A}}`
!!!

This will be replaced with the current time, in format of `A` in client's timezone.

| Token | Description | Example |
|-------|-------------|---------|
| `YYYY` | Full year | `2024` |
| `YY` | Two-digit year | `24` |
| `MM` | Month | `12` |
| `DD` | Day | `31` |
| `DDDD` | Day count of the year | `366` |
| `HH` | Hour (24-hour) | `23` |
| `hh` | Hour (12-hour) | `11` |
| `mm` | Minute | `59` |
| `ss` | Second | `59` |
| `A` | AM/PM indicator | `PM` |
| `X` | Unix timestamp | `1735689599` |
| `x` | Unix timestamp (ms) | `1735689599000` |

```text
{{time::YYYY-MM-DD HH:mm:ss}}
// Result: 2024-12-31 23:59:59
```

### `{{time::A::B}}`

!!!ghost Alias
`{{datetimeformat::A::B}}`, `{{date::A::B}}`
!!!

Same as `{{time::A}}`, but the time would be in the unix timestamp `B` instead of the current time.

+++ Message Time
### `{{message_time}}`

This will be replaced with the time when the message was sent.
The returned time format would determined by the browser or OS settings.

!!!warning Edge Cases
- Non-chat context or first message: `[Cannot get time]`
- Message from older version: `[Cannot get time, message was sent in older version]`
!!!

### `{{message_date}}`

This will be replaced with the date when the message was sent.
The returned date format would determined by the browser or OS settings.

!!!warning Edge Cases
- Non-chat context or first message: `[Cannot get time]`
- Message from older version: `[Cannot get time, message was sent in older version]`
!!!

### `{{message_idle_duration}}`

This will be replaced with the time when the user's previous message was sent subtracted by the time when the user's second previous message was sent.
The returned time format would be `HH:MM:SS` format.

!!!warning Edge Cases
- Non-chat context or first message: `[Cannot get time]`
- Message from older version: `[Cannot get time, message was sent in older version]`
- No previous messages: `[No user message found]`
!!!

### `{{idle_duration}}`

This will be replaced with the time when the user's previous message was sent subtracted by the current time.
The returned time format would be `HH:MM:SS` format.

### `{{message_unixtime_array}}`

This will be replaced with the array of unix timestamps of the chat log.
+++

---

## Emotion/Asset Syntaxes [!badge variant="success" text="Media"]

+++ Image & Video
### `{{asset::A}}`

This will be replaced with the element with the source of the additional asset path data named `A` of the current character. Type of the element would be determined by the asset type automatically.

### `{{emotion::A}}`

This will be replaced with the image element with the source of the emotion image path data named `A` of the current character.

### `{{image::A}}`

This will be replaced with the image element with the source of the additional asset path data named `A` of the current character.

### `{{img::A}}`

This will be replaced with the **unstyled** image element with the source of the additional asset path data named `A` of the current character.

### `{{video::A}}`

This will be replaced with the video element with the source of the additional asset path data named `A` of the current character.

### `{{video-img::A}}`

This will be replaced with the video element with the source of the additional asset path data named `A` of the current character. Unlike `{{video::A}}`, the element would be displayed like an image element.

+++ Audio & Background
### `{{audio::A}}`

This will be replaced with the audio element with the source of the additional asset path data named `A` of the current character.

### `{{bg::A}}`

This will be replaced with the background image element with the source of the additional asset path data named `A` of the current character.

+++ Utility
### `{{raw::A}}`

This will be replaced with additional asset path data named `A` of the current character.

### `{{assetlist}}`

This will be replaced with the array of names of additional assets of the current character.

### `{{emotionlist}}`

This will be replaced with the array of names of emotion images of the current character.

### `{{source::A}}`

This will be replaced with the path of the icon.

| Parameter | Description |
|-----------|-------------|
| `char` | Path of the character's icon |
| `user` | Path of the user's icon |
+++

---

## Math Syntaxes [!badge variant="warning" text="Math"]

=== Primary Calculator: `{{? A}}`

!!!ghost Alias
`{{calc::A}}`
!!!

This will be replaced with the result of the calculation of the provided expression `A`.

```text
{{? 5+3}}
// Result: 8
```

You can nest other syntaxes in the expression.

### Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `A+B` | Addition | `5+3` → `8` |
| `A-B` | Subtraction | `8-3` → `5` |
| `A*B` | Multiplication | `4*3` → `12` |
| `A/B` | Division | `12/4` → `3` |
| `A%B` | Remainder (Modulo) | `10%3` → `1` |
| `A^B` | Power | `2^3` → `8` |

### Logical Operators

| Operator | Description | Alias |
|----------|-------------|-------|
| `A\|\|B` | OR | `\|` |
| `A&&B` | AND | `&` |
| `!A` | NOT | - |

### Comparison Operators

| Operator | Description | Alias |
|----------|-------------|-------|
| `A==B` | Equal | `=` |
| `A!=B` | Not equal | - |
| `A>B` | Greater than | - |
| `A>=B` | Greater than or equal | `≥` |
| `A<B` | Less than | - |
| `A<=B` | Less than or equal | `≤` |

### Variable Access

Use `$<name>` to get the value of a chat variable. The name should only contain alphanumeric characters and underscores.

```text
{{? $health - 10}}
```

!!!info Important
Boolean values are represented as `1` for `true` and `0` for `false`.
`{{? A}}` syntax is only for numeric and boolean values. For string comparisons, use `{{equal::A::B}}`.
!!!

===

+++ Comparison Functions
### `{{equal::A::B}}`

This will be replaced with `1` if `A` is equal to `B`, otherwise `0`. Unlike `{{? A}}`, this syntax works for any type of values.

### `{{not_equal::A::B}}`

!!!ghost Alias
`{{notequal::A::B}}`
!!!

This will be replaced with `1` if `A` is not equal to `B`, otherwise `0`.

### `{{greater::A::B}}`

This will be replaced with `1` if `A` is greater than `B`, otherwise `0`.

### `{{greater_equal::A::B}}`

!!!ghost Alias
`{{greaterequal::A::B}}`
!!!

This will be replaced with `1` if `A` is greater than or equal to `B`, otherwise `0`.

### `{{less::A::B}}`

This will be replaced with `1` if `A` is less than `B`, otherwise `0`.

### `{{less_equal::A::B}}`

!!!ghost Alias
`{{lessequal::A::B}}`
!!!

This will be replaced with `1` if `A` is less than or equal to `B`, otherwise `0`.

+++ Logical Functions
### `{{and::A::B}}`

This will be replaced with `1` if `A` and `B` are both `1`, otherwise `0`.

### `{{or::A::B}}`

This will be replaced with `1` if `A` or `B` is `1`, otherwise `0`.

### `{{not::A}}`

This will be replaced with `1` if `A` is `0`, otherwise `0`.

+++ Math Functions
### `{{remaind::A::B}}`

This will be replaced with the remainder of the division of `A` by `B`.

### `{{pow::A::B}}`

This will be replaced with `A` raised to the power of `B`.

### `{{floor::A}}`

This will be replaced with the largest integer less than or equal to `A`.

### `{{ceil::A}}`

This will be replaced with the smallest integer greater than or equal to `A`.

### `{{abs::A}}`

This will be replaced with the absolute value of `A`.

### `{{round::A}}`

This will be replaced with `A` rounded to the nearest integer.

+++ Aggregate Functions
### `{{min::A::B::C...}}`

This will be replaced with the smallest value among `A`, `B`, `C`, and so on.

!!!tip Single Parameter
If only one parameter is provided, `A` will be treated as an array.
!!!

### `{{max::A::B::C...}}`

This will be replaced with the largest value among `A`, `B`, `C`, and so on.

!!!tip Single Parameter
If only one parameter is provided, `A` will be treated as an array.
!!!

### `{{sum::A::B::C...}}`

This will be replaced with the sum of `A`, `B`, `C`, and so on.

!!!tip Single Parameter
If only one parameter is provided, `A` will be treated as an array.
!!!

### `{{average::A::B::C...}}`

This will be replaced with the average of `A`, `B`, `C`, and so on.

!!!tip Single Parameter
If only one parameter is provided, `A` will be treated as an array.
!!!

### `{{fix_number::A::B}}`

This will be replaced with `A` with the number of decimal places fixed to `B`.
+++

---

## String Syntaxes [!badge variant="secondary" text="String"]

+++ Checks
### `{{startswith::A::B}}`

Returns `1` if `A` starts with `B`, otherwise `0`.

### `{{endswith::A::B}}`

Returns `1` if `A` ends with `B`, otherwise `0`.

### `{{contains::A::B}}`

Returns `1` if `A` contains `B`, otherwise `0`.

+++ Transformations
### `{{lower::A}}`

Converts `A` to lowercase.

### `{{upper::A}}`

Converts `A` to uppercase.

### `{{capitalize::A}}`

Capitalizes the first letter of `A`.

### `{{trim::A}}`

Removes leading and trailing whitespaces from `A`.

+++ Encoding
### `{{unicode_encode::A}}`

Encodes `A` to unicode. The result would be in the format of number.

### `{{unicode_decode::A}}`

Decodes `A` from unicode. The input should be in the format of number.
+++

---

## Conditional Syntaxes [!badge variant="danger" text="Logic"]

### `{{prefill_supported}}`

Returns `1` if the model supports prefilling, otherwise `0`.

### `{{jbtoggled}}`

Returns the current state of the jailbreak toggle. If jailbreak is enabled, returns `1`, otherwise `0`.

### `{{isfirstmsg}}`

Returns `1` if the message is the first message in the chat, otherwise `0`.

### `{{all::A::B::C...}}`

Returns `1` if **all** of the parameters are `1`, otherwise `0`.

!!!tip Single Parameter
If only one parameter is provided, `A` will be treated as an array.
!!!

### `{{any::A::B::C...}}`

Returns `1` if **any** of the parameters are `1`, otherwise `0`.

!!!tip Single Parameter
If only one parameter is provided, `A` will be treated as an array.
!!!

### `{{module_enabled::A}}`

Returns `1` if the module with namespace `A` is enabled, otherwise `0`.

---

## Variable Syntaxes [!badge variant="light" text="Variables"]

+++ Chat Variables
### `{{getvar::A}}`

Returns the value of the chat variable `A`. If not defined, returns `null`.

### `{{setvar::A::B}}`

Sets the chat variable `A` to `B` and returns an empty string.

!!!warning Limitations
Only works in chat context and not in the first message.
If possible, it is recommended to use trigger script instead.
!!!

### `{{addvar::A::B}}`

Increments the chat variable `A` by `B` and returns an empty string.

```text
// If variable A is 5
{{addvar::A::3}}
// Variable A becomes 8
```

!!!warning Limitations
Only works in chat context and not in the first message.
!!!

+++ Temp Variables
### `{{settempvar::A::B}}`

Sets the temporary variable `A` to `B` and returns an empty string.

!!!info Performance
Temporary variables are only available in the current context and are not saved when the chat is closed, but they are performance optimized.
!!!

### `{{gettempvar::A}}`

Returns the value of the temporary variable `A`. If not defined, returns `null`.

+++ Global Variables
### `{{getglobalvar::A}}`

Returns the value of the global variable `A`. If not defined, returns `null`.
+++

---

## Array Syntaxes [!badge variant="primary" text="Array"]

+++ Creation & Info
### `{{array::A::B::C...}}`

Creates an array from `A`, `B`, `C`, and so on.

!!!info Separator
Currently array uses `§` as separator, but this might change in the future. It is recommended to use this syntax instead of using `§` directly.
!!!

### `{{array_length::A}}`

!!!ghost Alias
`{{arraylength::A}}`
!!!

Returns the length of array `A`. This does not work with strings.

### `{{length::A}}`

Returns the length of `A`. This does not work with arrays.

+++ Access & Modify
### `{{array_element::A::B}}`

Returns the element of array `A` at index `B`.

!!!info Index
- Starts from `0`
- Negative index counts from the end
- Out of range returns `null`
!!!

### `{{array_push::A::B}}`

Returns array `A` with element `B` pushed to the end.

### `{{array_pop::A}}`

Returns array `A` with the last element removed.

### `{{array_shift::A}}`

Returns array `A` with the first element removed.

### `{{array_splice::A::B::C::D...}}`

Returns array `A` with `C`, `D`, and so on inserted at index `B`.

### `{{array_assert::A::B::C}}`

Returns array `A` with element `C` inserted at index `B`.

+++ Transform
### `{{split::A::B}}`

Splits string `A` by separator `B` and returns an array.

### `{{join::A::B}}`

Joins array `A` with separator `B` and returns a string.

### `{{filter::A::B}}`

Filters array `A` with option `B`.

| Option | Description |
|--------|-------------|
| `nonempty` | Remove empty strings |
| `unique` | Remove duplicate elements |
| `all` | Both `nonempty` and `unique` |

### `{{range::A}}`

Returns an array of numbers from `0` to `A - 1`.
+++

---

## Dictionary Syntaxes [!badge variant="info" text="Dict"]

### `{{dict::A=B::C=D...}}`

!!!ghost Alias
`{{object::A=B::C=D...}}`, `{{o::A=B::C=D...}}`, `{{d::A=B::C=D...}}`
!!!

Creates a dictionary with keys `A`, `C` and values `B`, `D`.

### `{{dict_element::A::B}}`

!!!ghost Alias
`{{object_element::A::B}}`
!!!

Returns the value of key `B` in dictionary `A`.

### `{{dict_assert::A::B::C}}`

!!!ghost Alias
`{{object_assert::A::B::C}}`
!!!

Returns dictionary `A` with key `B` and value `C` inserted.

---

## Utility Syntaxes [!badge variant="ghost" text="Utility"]

+++ Slots & Positions
### `{{slot}}`

If used in prompt template, pipeline, or translator prompt: replaced with original slot content.
Otherwise, not replaced.

### `{{slot::A}}`

If used in `{{#each C D}}` block and `D` equals `A`: replaced with the current element.
Otherwise, not replaced.

### `{{position::A}}`

If used in prompt template: replaced with lorebooks using position `pt_<A>` (e.g., `pt_personality`).
If no corresponding lorebook exists, replaced with empty string.

+++ Random
### `{{random::A::B...}}`

!!!ghost Alias
`{{random:A,B...}}`
!!!

Returns a random value from the provided parameters.

```text
{{random::A::B::C}}
// Returns either A, B, or C
```

If no parameters provided, returns a random number between 0 and 1.

### `{{pick::A::B...}}`

!!!ghost Alias
`{{pick:A,B...}}`
!!!

Same as `{{random::A::B...}}`, but the seed is the same for the same message, making the result consistent.

!!!warning Requirement
At least one parameter is required. Does not work without parameters.
!!!

### `{{roll::A}}`

!!!ghost Alias
`{{roll:A}}`
!!!

Returns a random number between 1 and `A`. If `A` starts with `d`, the `d` is ignored (e.g., `d20` → random 1-20).

### `{{rollp::A}}`

!!!ghost Alias
`{{rollp:A}}`
!!!

Same as `{{roll::A}}`, but the seed is the same for the same message.

+++ String Operations
### `{{spread::A}}`

Joins array `A` elements with `::`. Useful for creating multi-parameter syntaxes from arrays.

```text
{{random::{{spread::{{array::chicken::pizza::hamburger}}}}}}
// Equivalent to: {{random::chicken::pizza::hamburger}}
```

### `{{replace::A::B::C}}`

Returns `A` with all occurrences of `B` replaced with `C`.

### `{{tonumber::A}}`

Trims all non-numeric characters except `.`. Does not guarantee a valid number result.

+++ Special
### `{{none}}`

!!!ghost Alias
`{{blank}}`
!!!

Returns an empty string. Useful for removing default text.

!!!tip First Message
If used in first message, the first message will work as if it doesn't exist.
!!!

### `{{br}}`

!!!ghost Alias
`{{newline}}`
!!!

Returns a line break.

### `{{return::A}}`

Replaces the entire message with `A` and ignores the rest.

+++ Functions
### `{{func::A::B::C...}}`

Calls the function `A` with arguments `B`, `C`, and so on.

### `{{arg::A}}`

Returns the argument at index `A` when called within a function.
+++

---

## Block Syntaxes [!badge variant="contrast" text="Block"]

=== `{{#if A}}`

Conditionally includes content based on the value of `A`.
Content is included if `A` equals `1`, otherwise replaced with empty string.

```text
{{#if {{equal::1::1}}}}
Hello Alice!
{{/if}}
```

===

### `{{#if-pure A}}`

Same as `{{#if A}}`, but **preserves** the indentation and whitespace of the content.

=== `{{#each A B}}`

Iterates over array `A`. Use `{{slot::B}}` to access the current element.

```text
{{#each {{array::chicken::pizza::hamburger}} item}}
{{slot::item}}
{{/each}}
```

**Result:**
```text
chickenpizzahamburger
```

===

### `{{#func A}}`

Defines a function named `A`. Can be called with `{{func::A::B::C...}}`.

### `{{#pure_display}}`

Displays the content without any formatting. Useful for displaying raw text.