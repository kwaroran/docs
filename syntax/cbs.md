# Curly Braced Syntaxes

Curly braced syntaxes (like `{{user}}`) are used to insert special values into the text.
The syntaxes can be used in almost any text field in the client, including chat messages, character descriptions, and lorebook entries.

The syntaxes are replaced with the actual values when the message is sent or when the text is displayed in the client.
The syntaxes can be nested and combined with other syntaxes, for example, `{{calc::{{getvar::a}}+{{getvar::b}}}}`.

The syntaxes are case-insensitive, so `{{user}}`, `{{User}}`, and `{{USER}}` are all the same.
Some of the syntaxes require parameters, which are separated by `::` (two colons).

Some of the syntaxes require arrays as parameters. use `{{array::A::B::C...}}` syntax to create an array.
Some of the syntaxes are block syntaxes (like `{{#if A}}`), which are started with `{{#NAME A}}` and ended with `{{/NAME}}`. The block syntaxes can be nested, and starts with `#`. it can also be closed with `{{/}}` instead of `{{/NAME}}`. block syntaxes's content's indentation and whitespace would be trimmed, unless for some syntaxes like `{{#if_pure A}}` which would keep the indentation and whitespace.

## Data Syntaxes

### `{{user}}`

This will be replaced with the personas's name.

### `{{char}}`

> Alias: `{{bot}}`

This will be replaced with the character's name.
If you are chatting in a group chat, if the speaker is user, this will be replaced with group chat name. if the speaker is character, this will be replaced with the speaker's name.

### `{{description}}`

> Alias: `{{char_desc}}`

This will be replaced with the character's description.

### `{{example_dialogue}}`

> Alias: `{{example_message}}`

This will be replaced with an array of example dialogue of the character.

### `{{persona}}`

> Alias: `{{user_persona}}`

This will be replaced with the persona's description.

### `{{lorebook}}`

> Alias: `{{world_info}}`

This will be replaced with array of lorebook entries.

### `{{authornote}}`

> Alias: `{{author_note}}`

This will be replaced with [Author's Note](/characterconfig/basic.md) included in the current chat prompt. This is also known as memory or UJB.

### `{{history}}`

> Alias: `{{messages}}`

This will be replaced with array of messages in current chat.

### `{{chat_index}}`

This will be replaced with the index of the message in the chat.
The chat index starts from 0 except for the first message. The first message has an index of -1.
If the `{{chat_index}}` is used in non-chat context, it will be replaced with -1.

### `{{model}}`

This will be replaced with the current model id of the client.

### `{{axmodel}}`

This will be replaced with the current auxiliary model id of the client.

### `{{role}}`

This will be replaced with the current role of the message sender.
If the `{{role}}` is used in non-chat context, it will be replaced with `role` string.

### `{{maxcontext}}`

This will be replaced with the maximum context length setting of the client.

### `{{lastmessage}}`

This will be replaced with the last message in the chat log.

### `{{lastmessageid}}`

> Alias: `{{lastmessageindex}}`

This will be replaced with the index of the last message in the chat log.

### `{{previous_char_chat}}`

> Alias: `{{lastcharmessage}}`

This will be replaced with the last message of the current character in the chat log.

### `{{previous_user_chat}}`

> Alias: `{{lastusermessage}}`

This will be replaced with the last message of the user in the chat log.

### `{{previous_chat_log::A}}`

This will be replaced with the chat message with the index of `A` in the chat log. If the message does not exist, it will be replaced with `Out of range`

### `{{first_msg_index}}`

This will be replaced with the index of the first message in the chat log.

### `{{screen_width}}`

This will be replaced with the width of the screen in pixels.

### `{{screen_height}}`

This will be replaced with the height of the screen in pixels.

### `{{user_history}}`

This will be replaced with the array of messages of the user in the chat log.

### `{{char_history}}`

This will be replaced with the array of messages of the character in the chat log.

## Time Syntaxes

### `{{time}}`

This will be replaced with the current time in the client's timezone. The returned value is not zero-padded, so it may look like `9:5:3`.

### `{{time::A}}`

This will be replaced with the current time, in format of `A` in client's timezone.

The format `A` can include the following:
- `YYYY` for the year.
- `YY` for the year in two digits.
- `MM` for the month.
- `DD` for the day.
- `DDDD` for the day count of the year.
- `HH` for the hour, in 24-hour format.
- `hh` for the hour, in 12-hour format.
- `mm` for the minute.
- `ss` for the second.
- `A` for the AM/PM indicator.
- `X` for the unix timestamp.
- `x` for the unix timestamp in milliseconds.

for example, `{{time::YYYY-MM-DD HH:mm:ss}}` will be replaced with the current time in the format `2024-12-31 23:59:59` if the current time is `2024-12-31 23:59:59`.

### `{{time::A::B}}`

Same as `{{time::A}}`, but the time is based on timestamp `B` in milliseconds instead of the current time.

### `{{unixtime}}`

This will be replaced with the current Unix timestamp in seconds.

### `{{date}}`

> Alias: `{{datetimeformat}}`

This will be replaced with the current date, in the format `YYYY-M-D` in client's timezone.

### `{{isotime}}`

This will be replaced with the current time, in the format `HH:MM:SS` in the UTC timezone.

### `{{isodate}}`

This will be replaced with the current date, in the format `YYYY-MM-DD` in the UTC timezone.

### `{{message_time}}`

This will be replaced with the time when the message was sent.
The returned time format would determined by the browser or OS settings.

If the `{{message_time}}` is used in non-chat context or the first message, it will be replaced [Cannot get time] string.
If the message was sent before `{{message_time}}` syntax was introduced, it will be replaced with [Cannot get time, message was sent in older version] string.

### `{{message_date}}`

This will be replaced with the date when the message was sent.
The returned date format would determined by the browser or OS settings.

If the `{{message_date}}` is used in non-chat context or the first message, it will be replaced [Cannot get time] string.
If the message was sent before `{{message_date}}` syntax was introduced, it will be replaced with [Cannot get time, message was sent in older version] string.

### `{{message_idle_duration}}`

This will be replaced with the time when the user's previous message was sent subtracted by the time when the user's second previous message was sent.
The returned time format would be `HH:MM:SS` format.

If the `{{message_idle_duration}}` is used in non-chat context or the first message, it will be replaced [Cannot get time] string.
If the message was sent before `{{message_idle_duration}}` syntax was introduced, it will be replaced with [Cannot get time, message was sent in older version] string.
If there are no previous messages, it will be replaced with [No user message found] string.

### `{{idle_duration}}`

This will be replaced with the time when the user's previous message was sent subtracted by the current time.
The returned time format would be `HH:MM:SS` format.

### `{{message_unixtime_array}}`

This will be replaced with the array of unix timestamps of the chat log.

## Emotion/Asset Syntaxes

### `{{asset::A}}`

This will be replaced with the element with the source of the additional asset path data named `A` of the current character. type of the element would be determined by the asset type automatically.

### `{{emotion::A}}`

This will be replaced with the image element with the source of the emotion image path data named `A` of the current character.

### `{{audio::A}}`

This will be replaced with the audio element with the source of the additional asset path data named `A` of the current character.

### `{{bg::A}}`

This will be replaced with the background image element with the source of the additional asset path data named `A` of the current character.

### `{{video::A}}`

This will be replaced with the video element with the source of the additional asset path data named `A` of the current character.

### `{{video-img::A}}`

This will be replaced with the video element with the source of the additional asset path data named `A` of the current character. unlike `{{video::A}}`, the element would be displayed like an image element.

### `{{raw::A}}`

This will be replaced with additional asset path data named `A` of the current character.

### `{{image::A}}`

This will be replaced with the image element with the source of the additional asset path data named `A` of the current character.

### `{{img::A}}`

This will be replaced with the unstyled image element with the source of the additional asset path data named `A` of the current character.

### `{{assetlist}}`

This will be replaced with the array of names of additional assets of the current character.

### `{{chardisplayasset}}`

This will be replaced with a JSON array of asset names inserted into the prompt for character display assets. Unlike `{{assetlist}}`, this reflects the New Image Handling setting and excludes assets disabled for prompt insertion.

### `{{moduleassetlist::A}}`

> Alias: `{{module_assetlist::A}}`

This will be replaced with an array of asset names from module namespace `A`. If the module is not found, this will be replaced with an empty string.

### `{{emotionlist}}`

This will be replaced with the array of names of emotion images of the current character.

### `{{source::A}}`

This will be replaced with the path of the icon. if A is `char`, it will be replaced with the path of the character's icon. if A is `user`, it will be replaced with the path of the user's icon.

### `{{inlay::A}}`

This displays unstyled inlay asset `A`. The asset is not inserted into the model request.

### `{{inlayed::A}}`

This displays styled inlay asset `A`. The asset is not inserted into the model request.

### `{{inlayeddata::A}}`

This displays styled inlay asset `A`. The asset is inserted into the model request.

## Math Syntaxes

### `{{? A}}`

>Alias: `{{calc::A}}`

This will be replaced with the result of the calculation of the provided expression `A`. for example, `{{? 5+3}}` will be replaced with `8`. You can nest other syntaxes in the expression.

These are the supported operators and functions:
- `A+B` for addition of `A` and `B`.
- `A-B` for subtraction of `B` from `A`.
- `A*B` for multiplication of `A` and `B`.
- `A/B` for division of `A` by `B`.
- `A%B` for remainder of the division of `A` by `B`.
- `A^B` for `A` raised to the power of `B`.
- `A||B` for `A` or `B`.
- `A&&B` for `A` and `B`.
- `!A` for not `A`.
- `A==B` for `A` is equal to `B`.
- `A!=B` for `A` is not equal to `B`.
- `A>B` for `A` is greater than `B`.
- `A>=B` for `A` is greater than or equal to `B`.
- `A<B` for `A` is less than `B`.
- `A<=B` for `A` is less than or equal to `B`.
- `$<name>` for getting the value of the chat variable named `<name>`. `<name>` should be named with only alphanumeric characters and underscore.

Some of the syntaxes has aliases:
- `|` for `||`
- `&` for `&&`
- `=` for `==`
- `≤` for `<=`
- `≥` for `>=`

The boolean values are represented as `1` for `true` and `0` for `false`. Note that `{{? A}}` syntax is only for numeric and boolean values. for string values, use other syntaxes like `{{equal::A::B}}`.

### `{{equal::A::B}}`

This will be replaced with `1` if `A` is equal to `B`, otherwise it will be replaced with `0`. unlike `{{? A}}`, this syntax works for any type of values.

### `{{not_equal::A::B}}`

> Alias: {{notequal::A::B}}

This will be replaced with `1` if `A` is not equal to `B`, otherwise it will be replaced with `0`. unlike `{{? A}}`, this syntax works for any type of values.

### `{{remaind::A::B}}`

This will be replaced with the remainder of the division of `A` by `B`.

### `{{greater::A::B}}`

This will be replaced with `1` if `A` is greater than `B`, otherwise it will be replaced with `0`.

### `{{greater_equal::A::B}}`

> Alias: {{greaterequal::A::B}}

This will be replaced with `1` if `A` is greater than or equal to `B`, otherwise it will be replaced with `0`.

### `{{less::A::B}}`

This will be replaced with `1` if `A` is less than `B`, otherwise it will be replaced with `0`.

### `{{less_equal::A::B}}`

> Alias: {{lessequal::A::B}}

This will be replaced with `1` if `A` is less than or equal to `B`, otherwise it will be replaced with `0`.

### `{{and::A::B}}`

This will be replaced with `1` if `A` and `B` are both `1`, otherwise it will be replaced with `0`.

### `{{or::A::B}}`

This will be replaced with `1` if `A` or `B` is `1`, otherwise it will be replaced with `0`.

### `{{pow::A::B}}`

This will be replaced with `A` raised to the power of `B`.

### `{{not::A}}`

This will be replaced with `1` if `A` is `0`, otherwise it will be replaced with `0`.

### `{{floor::A}}`

This will be replaced with the largest integer less than or equal to `A`.

### `{{ceil::A}}`

This will be replaced with the smallest integer greater than or equal to `A`.

### `{{abs::A}}`

This will be replaced with the absolute value of `A`.

### `{{round::A}}`

This will be replaced with `A` rounded to the nearest integer.

### `{{min::A::B::C...}}`

This will be replaced with the smallest value among `A`, `B`, `C`, and so on.
If only one parameter is provided, `A` will be treated as the array of values.

### `{{max::A::B::C...}}`

This will be replaced with the largest value among `A`, `B`, `C`, and so on.
If only one parameter is provided, `A` will be treated as the array of values.

### `{{sum::A::B::C...}}`

This will be replaced with the sum of `A`, `B`, `C`, and so on.
If only one parameter is provided, `A` will be treated as the array of values.

### `{{average::A::B::C...}}`

This will be replaced with the average of `A`, `B`, `C`, and so on.
If only one parameter is provided, `A` will be treated as the array of values.

### `{{fix_number::A::B}}`

This will be replaced with `A` with the number of decimal places fixed to `B`.

### `{{randint::A::B}}`

This will be replaced with a random integer between `A` and `B`, inclusive. If `A` or `B` is not a valid number, this will be replaced with `NaN`.

### `{{dice::A}}`

This will roll dice using standard dice notation. For example, `{{dice::2d6}}` rolls two six-sided dice and returns the sum.

### `{{fromhex::A}}`

This will be replaced with hexadecimal value `A` converted to a decimal number.

### `{{tohex::A}}`

This will be replaced with decimal value `A` converted to a hexadecimal string.

## String Syntaxes

### `{{startswith::A::B}}`

This will be replaced with `1` if `A` starts with `B`, otherwise it will be replaced with `0`.

### `{{endswith::A::B}}`

This will be replaced with `1` if `A` ends with `B`, otherwise it will be replaced with `0`.

### `{{contains::A::B}}`

This will be replaced with `1` if `A` contains `B`, otherwise it will be replaced with `0`.

### `{{lower::A}}`

This will be replaced with `A` converted to lowercase.

### `{{upper::A}}`

This will be replaced with `A` converted to uppercase.

### `{{capitalize::A}}`

This will be replaced with `A` with the first letter capitalized.

### `{{trim::A}}`

This will be replaced with `A` with leading and trailing whitespaces removed.

### `{{unicode_encode::A}}`

This will be replaced with `A` encoded to unicode. the result would be in the format of number

### `{{unicode_decode::A}}`

This will be replaced with `A` decoded from unicode. the input should be in the format of number

### `{{unicodedecodefromhex::A}}`

> Alias: `{{u::A}}`

This will be replaced with the character represented by hexadecimal Unicode code `A`.

### `{{unicodeencodefromhex::A}}`

> Alias: `{{ue::A}}`

This works the same as `{{u::A}}`.

### `{{xorencrypt::A}}`

> Alias: `{{xor::A}}`, `{{xorencode::A}}`, `{{xore::A}}`

This will encrypt `A` with a simple XOR cipher and encode the result as base64.

### `{{xordecrypt::A}}`

> Alias: `{{xordecode::A}}`, `{{xord::A}}`

This will decrypt a base64-encoded value created by `{{xor::A}}`.

### `{{crypt::A}}`

> Alias: `{{crypto::A}}`, `{{caesar::A}}`, `{{encrypt::A}}`, `{{decrypt::A}}`

This will apply a Caesar cipher to `A`. With no second argument, it uses the default shift value.

### `{{crypt::A::B}}`

> Alias: `{{crypto::A::B}}`, `{{caesar::A::B}}`, `{{encrypt::A::B}}`, `{{decrypt::A::B}}`

This will apply a Caesar cipher to `A` using shift value `B`.

Example:
```
{{crypt::Hello, World!}}
{{crypt::聈聥聬聬聯耬耠聗聯聲聬聤耡}}

{{crypt::Hello, World!::3}}
{{crypt::Khoor/#Zruog$::-3}}
```

will be replaced with
```
聈聥聬聬聯耬耠聗聯聲聬聤耡
Hello, World!

Khoor/#Zruog$
Hello, World!
```

## Conditional Syntaxes

### `{{prefill_supported}}`

This will be replaced with `1` if the model supports prefilling, otherwise it will be replaced with `0`.

### `{{jbtoggled}}`

This will be replaced with the current state of the jailbreak toggle.
If jailbreak is enabled, it will be replaced with `1`, otherwise it will be replaced with `0`.

### `{{isfirstmsg}}`

This will be replaced with `1` if the message is the first message in the chat, otherwise it will be replaced with `0`.

### `{{all::A::B::C...}}`

This will be replaced with `1` if all of the parameters are `1`, otherwise it will be replaced with `0`.
If only one parameter is provided, `A` will be treated as the array of values.

### `{{any::A::B::C...}}`

This will be replaced with `1` if any of the parameters are `1`, otherwise it will be replaced with `0`.
If only one parameter is provided, `A` will be treated as the array of values.

### `{{module_enabled::A}}`

This will be replaced with `1` if the module with namespace `A` is enabled, otherwise it will be replaced with `0`.

### `{{iserror::A}}`

This will be replaced with `1` if `A` starts with `error:`, otherwise it will be replaced with `0`. The check is case-insensitive.

## Variable Syntaxes

### `{{getvar::A}}`

This will be replaced with the value of the chat variable `A`. If the chat variable `A` is not defined, it will be replaced with `null`.

### `{{setvar::A::B}}`

This will set the chat variable `A` to `B` and be replaced with an empty string. `{{setvar::A::B}}` only works when it is in the chat context and it is not the first message.

If its possible, it is recommended to use trigger script instead of this syntax.

### `{{addvar::A::B}}`

This will increment the chat variable `A` by `B` and be replaced with an empty string. for example, if variable `A` is `5` and `{{addvar::A::3}}` is used, the variable `A` will be `8`. `{{addvar::A::B}}` only works when it is in the chat context and it is not the first message.

### `{{settempvar::A::B}}`

This will set the temporary variable `A` to `B` and be replaced with an empty string. `{{settempvar::A::B}}` only works when it is in the chat context and it is not the first message.

Temporary variables are only available in the current context and are not saved when the chat is closed, however, it is performance optimized.

### `{{gettempvar::A}}`

This will be replaced with the value of the temporary variable `A`. If the temporary variable `A` is not defined, it will be replaced with `null`.

### `{{getglobalvar::A}}`

This will be replaced with the value of the global variable `A`. If the global variable `A` is not defined, it will be replaced with `null`.

## Array Syntaxes

### `{{array::A::B::C...}}`

This will be replaced with an array of `B`, `C`, and so on. This can be used to create an array from multiple parameters.

For compatibility, strings that are not JSON arrays may be split by `§`, but using `§` directly is not recommended.

### `{{array_length::A}}`

> Alias: {{arraylength::A}}

This will be replaced with the length of array `A`. this would not work with strings.

### `{{array_element::A::B}}`

This will be replaced with the element of array `A` at index `B`.
index starts from 0. if the index is out of range, it will be replaced with `null`. if index is negative, it will be counted from the end of the array.

### `{{array_push::A::B}}`

This will be replaced with array `A` with element `B` pushed to the end.

### `{{array_pop::A}}`

This will be replaced with array `A` with the last element removed.

### `{{array_shift::A}}`

This will be replaced with array `A` with the first element removed.

### `{{array_splice::A::B::C::D}}`

This will be replaced with array `A` after removing `C` elements starting at index `B` and inserting element `D` at that position.

### `{{array_assert::A::B::C}}`

This will be replaced with array `A` with element `C` inserted at index `B`.

### `{{split::A::B}}`

This will be replaced with an array of strings that are separated by `B` in `A`.

### `{{join::A::B}}`

This will be replaced with a string that is created by joining the elements of array `A` with `B`.

### `{{filter::A::B}}`

This will be replaced with array `A` with elements filtered. the filter `B` is the option.
options are:
- `nonempty`: remove empty strings.
- `unique`: remove duplicate elements.
- `all`: perform both `nonempty` and `unique` filter.

### Dictionary Syntaxes

### `{{dict::A=B::C=D...}}`

> Alias: `{{object::A=B::C=D...}}`, `{{o::A=B::C=D...}}`, `{{d::A=B::C=D...}}`

This will be replaced with a dictionary with keys `A`, `C`, and so on and values `B`, `D`, and so on.

### `{{dict_element::A::B}}`

> Alias: `{{object_element::A::B}}`

This will be replaced with the value of the key `B` in dictionary `A`.

### `{{dict_assert::A::B::C}}`

> Alias: `{{object_assert::A::B::C}}`

This will be replaced with dictionary `A` with key `B` and value `C` inserted.

## Utility Syntaxes

### `{{slot}}`

It is replaced only in specific contexts such as prompt templates, group templates, translator prompts, summarization prompts, image prompts, and some trigger/lore operations. In normal chat parsing, it is left unchanged.

### `{{slot::A}}`

Inside a `{{#each C as A}}` block, this is replaced with the current element of array `C`. If the name does not match the loop variable, it is left unchanged.

### `{{position::A}}`

If it is used in prompt template, it will be replaced to the lorebooks that uses position `pt_<A>` like `pt_personality`. if the corresponding lorebook does not exist, it will be replaced with an empty string. otherwise, it will not be replaced.

### `{{random::A::B...}}`

> Alias: `{{random:A,B...}}`

This will be replaced with a random value from the provided parameters. for example, `{{random::A::B::C}}` will be replaced with either `A`, `B`, or `C`.
If no parameters are provided, it will be replaced with random number between 0 and 1.

### `{{pick::A::B...}}`

> Alias: `{{pick:A,B...}}`

This would work same as `{{random::A::B...}}`, except the seed would be the same for the same message which would make the result consistent. This also doesn't work with no parameters.

### `{{roll::A}}`

> Alias: `{{roll:A}}`

This will be replaced with a random number between 1 and `A`. if `A` starts with `d`, it will be replaced with a random number between 1 and `A` without the `d`.

### `{{rollp::A}}`

> Alias: `{{rollp:A}}`, `{{rollpick::A}}`

This would work same as `{{roll::A}}`, except the seed would be the same for the same message which would make the result consistent.

### `{{spread::A}}`

This will be replaced with a a string created by joining the elements of array `A` with `::` (two colons). This can be used to make multi-parameter syntaxes from arrays. For example, `{{random::{{spread::{{array::chicken::pizza::hamburger}}}}}}` will act same as `{{random::chicken::pizza::hamburger}}`.

### `{{replace::A::B::C}}`

This will be replaced with `A` with all occurrences of `B` replaced with `C`.

### `{{range::A}}`

This will be replaced with an array of numbers from 0 to `A` - 1.

### `{{length::A}}`

This will be replaced with the length of `A`. this would not work with arrays.

### `{{tonumber::A}}`

This would trim all non-numeric characters except for `.`. This doesn't guarantee that the result is a valid number.

### `{{return::A}}`

If this syntax is provided, the message will be replaced with `A` and the rest of the message will be ignored.

### `{{button::A::B}}`

This will add a button HTML element with label `A`. When clicked, it runs trigger `B`. See the [Trigger Script (Lua Mode)](/srp/lua.md) documentation for trigger behavior.

### `{{risu}}`

This will add the Risu icon at the default size.

### `{{risu::A}}`

This will add the Risu icon with width and height set to `A` pixels.

### `{{call::A::B::C...}}`

This calls the function block named `A` with arguments `B`, `C`, and so on, and is replaced with the function result.

### `{{hash::A}}`

This will be replaced with a deterministic 7-digit number generated from `A`. The same input always returns the same output.

### `{{metadata::A}}`

This will be replaced with metadata value `A`.

<details>
<summary>Supported metadata keys</summary>

| Key | Description |
| --- | --- |
| `mobile` | Returns `1` in a mobile environment, otherwise `0`. |
| `local` | Returns `1` in a local app environment, otherwise `0`. |
| `node` | Returns `1` in a Node server environment, otherwise `0`. |
| `version` | Returns the app version. |
| `majorversion`, `majorver`, `major` | Returns only the first number of the app version. |
| `language`, `locale`, `lang` | Returns the language value configured in the app. |
| `browserlanguage`, `browserlocale`, `browserlang` | Returns the browser language value. |
| `modelshortname` | Returns the short name of the current model. |
| `modelname` | Returns the current model name. |
| `modelinternalid` | Returns the internal ID of the current model. |
| `modelformat` | Returns the format value of the current model. |
| `modelprovider` | Returns the provider value of the current model. |
| `modeltokenizer` | Returns the tokenizer value of the current model. |
| `risutype` | Returns the runtime environment as one of `local`, `node`, or `web`. |
| `maxcontext` | Returns the current maximum context length. |

</details>

If `A` is not a valid metadata key, this will be replaced with an error string.

### `{{hiddenkey::A}}`

This works as a hidden key for activating lorebook entries while keeping `A` out of the model request.

### `{{// A}}`

This is a comment syntax. It can be used to comment out CBS code.

### `{{comment::A}}`

This is a visible comment syntax. Unlike `{{// A}}`, the comment content is displayed in the chat.

### Escaping Syntaxes

### `{{none}}`

> Alias: `{{blank}}`

This will be replaced with an empty string. Useful for removing the default text.

If its used in first message, the first message will work as if it not exists.

### `{{br}}`

> Alias: `{{newline}}`

This will be replaced with a line break.

### `{{cbr}}`

> Alias: `{{cnl}}`, `{{cnewline}}`

This will be replaced with a line break character `\n` without actually creating a new line in the output.

### `{{displayescapedcurlybracketopen}}`

> Alias: `{{decbo}}`

This will be replaced with a special character that displays as `{` but is not parsed as CBS syntax.

### `{{displayescapedcurlybracketclose}}`

> Alias: `{{decbc}}`

This will be replaced with a special character that displays as `}` but is not parsed as CBS syntax.

### `{{doubledisplayescapedcurlybracketopen}}`

> Alias: `{{ddecbo}}`, `{{bo}}`

This will be replaced with special characters that display as `{{` but are not parsed as CBS syntax.

### `{{doubledisplayescapedcurlybracketclose}}`

> Alias: `{{ddecbc}}`, `{{bc}}`

This will be replaced with special characters that display as `}}` but are not parsed as CBS syntax.

### `{{displayescapedbracketopen}}`

> Alias: `{{debo}}`, `{{(}}`

This will be replaced with a special character that displays as `(` without interfering with parsing.

### `{{displayescapedbracketclose}}`

> Alias: `{{debc}}`, `{{)}}`

This will be replaced with a special character that displays as `)` without interfering with parsing.

### `{{displayescapedanglebracketopen}}`

> Alias: `{{deabo}}`, `{{<}}`

This will be replaced with a special character that displays as `<` without interfering with HTML parsing.

### `{{displayescapedanglebracketclose}}`

> Alias: `{{deabc}}`, `{{>}}`

This will be replaced with a special character that displays as `>` without interfering with HTML parsing.

### `{{displayescapedcolon}}`

> Alias: `{{dec}}`, `{{:}}`

This will be replaced with a special character that displays as `:` but is not parsed as a CBS argument separator.

### `{{displayescapedsemicolon}}`

> Alias: `{{;}}`

This will be replaced with a special character that displays as `;` without interfering with parsing.

### Rendering Syntaxes

### `{{tex::A}}`

> Alias: `{{latex::A}}`, `{{katex::A}}`

This will render `A` as a LaTeX math expression.

### `{{ruby::A::B}}`

> Alias: `{{furigana::A::B}}`

This will render ruby text for East Asian typography. `A` is the base text and `B` is the ruby text.

### `{{codeblock::A}}`

This will render `A` as a code block.

### `{{codeblock::A::B}}`

This will render `B` as a code block with language `A` for syntax highlighting.

### `{{bkspc}}`

This removes the last word from the current output.

### `{{erase}}`

This removes the last sentence from the current output.

## Block Syntaxes

### `{{#if A}}`

This will be replaced with the `content` if `A` is `1`, otherwise it will be replaced with an empty string.

Example:
```
{{#if {{equal::1::1}}}}
Hello Alice!
{{/if}}
```

### `{{#if_pure A}}`

Same as `{{#if A}}`, but it would keep the indentation and whitespace of the content.


### `{{#each A as B}}`

Parses `A` as an array and repeats the block content for each element. Inside the block, `{{slot::B}}` is replaced with the current element.

Compatibility form `{{#each A B}}` is also supported, but `{{#each A as B}}` is preferred.

Use `{{#each::keep A as B}}` to preserve whitespace inside the block.

Example:
```
{{#each {{array::chicken::pizza::hamburger}} as item}}
{{slot::item}}
{{/each}}
```

will be replaced with
```
chickenpizzahamburger
```

<style>
    h2, h3 {
        margin-top: 4rem !important;
    }
</style>

### `{{#func A}}`

This defines a function block named `A`. The block can be called with `{{call::A::B::C...}}`.

Inside the function block, use `{{arg::N}}` to read an argument passed by `{{call}}`. `{{arg::0}}` is the function name, so user-provided arguments start from `{{arg::1}}`.

Example:
```
{{#func greet}}
Hello, {{arg::1}}!
{{/func}}
{{call::greet::Alice}}
```

Output:
```
Hello, Alice!
```

### `{{#pure_display}}`

This will be replaced with the `content` without any formatting. This is useful for displaying raw text.

### `{{#when A}}`

This will include the block content if `A` is truthy. `1` and `true` are treated as true; other values are treated as false.

`#when` can also use operators with `::`, such as `and`, `or`, `is`, `isnot`, `>`, `<`, `>=`, `<=`, and `not`.

Example:
```
{{#when::A::and::B}}
Content
{{/when}}
```

Advanced operators include `keep` for preserving whitespace, `legacy` for old `#if`-style whitespace handling, `var` for checking a variable, and `toggle` for checking a toggle.

### `{{:else}}`

This is an else branch for `{{#when}}`. It is used inside a `#when` block.

Example:
```
{{#when A}}
If A is true
{{:else}}
If A is false
{{/when}}
```

### `{{#escape}}`

This will treat the block content as literal text by escaping curly braces and parentheses, so CBS syntax inside the block is not evaluated.

Use `{{#escape::keep}}` to preserve whitespace inside the block.

### `{{#puredisplay}}`

This is useful for displaying raw CBS syntax, HTML, or other content without parsing.

### `{{#pure}}`

This displays the block content without CBS processing.

This is an old syntax and is deprecated. Use `{{#puredisplay}}` instead.
