# Curly Braced Syntaxes

Curly braced syntaxes (like `{{user}}`) are used to insert special values into the text.
The syntaxes can be used in almost any text field in the client, including chat messages, character descriptions, and lorebook entries.

The syntaxes are replaced with the actual values when the message is sent or when the text is displayed in the client.
The syntaxes can be nested and combined with other syntaxes, for example, `{{calc::{{getvar::a}}+{{getvar::b}}}}`.

The syntaxes are case-insensitive, so `{{user}}`, `{{User}}`, and `{{USER}}` are all the same.
Some of the syntaxes require parameters, which are separated by `::` (two colons).

Some of the syntaxes require arrays as parameters, which a string separated by `§` (section sign) like `chicken§pizza§hamburger`.
Some of the syntaxes are block syntaxes (like `{{#if}}`), which are started with `{{#NAME A}}` and ended with `{{/NAME}}`. The block syntaxes can be nested, and starts with `#`. it can also be closed with `{{/}}` instead of `{{/NAME}}`.

## Syntax List


### `{{user}}`

This will be replaced with the personas's name.

### `{{char}}`

This will be replaced with the character's name.
If you are chatting in a group chat, if the speaker is user, this will be replaced with group chat name.
if the speaker is character, this will be replaced with the speaker's name.


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

### `{{history}}`

> Alias: `{{messages}}`

This will be replaced with array of messages in current chat.

### `{{chat_index}}`

This will be replaced with the index of the message in the chat.
The chat index starts from 0 except for the first message. The first message has an index of -1.
If the `{{chat_index}}` is used in non-chat context, it will be replaced with -1.

### `{{none}}`

> Alias: `{{blank}}`

This will be replaced with an empty string. Useful for removing the default text.

### `{{time}}`

This will be replaced with the current time, in the format `HH:MM:SS` in client's timezone.

### `{{date}}`

This will be replaced with the current date, in the format `YYYY-MM-DD` in client's timezone.

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

If the `{{{message_date}}` is used in non-chat context or the first message, it will be replaced [Cannot get time] string.
If the message was sent before `{{message_date}}` syntax was introduced, it will be replaced with [Cannot get time, message was sent in older version] string.

### `{{idle_duration}}`

This will be replaced with the time when the user's previous message was sent subtracted by the time when the user's second previous message was sent.
The returned time format would be `HH:MM:SS` format.

If the `{{idle_duration}}` is used in non-chat context or the first message, it will be replaced [Cannot get time] string.
If the message was sent before `{{idle_duration}}` syntax was introduced, it will be replaced with [Cannot get time, message was sent in older version] string.
If there are no previous messages, it will be replaced with [No user message found] string.

### `{{br}}`

> Alias: `{{newline}}`

This will be replaced with a line break.

### `{{model}}`

This will be replaced with the current model id of the client.

### `{{axmodel}}`

This will be replaced with the current auxiliary model id of the client.

### `{{role}}`

This will be replaced with the current role of the message sender.
If the `{{role}}` is used in non-chat context, it will be replaced with `role` string.

### `{{jbtoggled}}`

This will be replaced with the current state of the jailbreak toggle.
If jailbreak is enabled, it will be replaced with `1`, otherwise it will be replaced with `0`.

### `{{maxprompt}}`

This will be replaced with the maxinum tokens setting of the client.

### `{{slot}}`

If it is used in prompt template, pipeline or translator prompt, it will be replaced to original slot content. otherwise, it will not be replaced.

### `{{random::A::B...}}`

> Alias: `{{random:A,B...}}`

This will be replaced with a random value from the provided parameters. for example, `{{random::A::B::C}}` will be replaced with either `A`, `B`, or `C`.
If no parameters are provided, it will be replaced with random number between 0 and 1.

### `{{pick::A::B...}}`

> Alias: `{{pick:A,B...}}`

This would work same as `{{random::A::B...}}`, except the seed would be the same for the same message which would make the result consistent. This also doesn't work with no parameters.

### `{{getvar::A}}`

This will be replaced with the value of the chat variable `A`. If the chat variable `A` is not defined, it will be replaced with `null`.

### `{{setvar::A::B}}`

This will set the chat variable `A` to `B` and be replaced with an empty string. `{{setvar::A::B}}` only works when it is in the chat context and it is not the first message.

### `{{addvar::A::B}}`

This will increment the chat variable `A` by `B` and be replaced with an empty string. for example, if variable `A` is `5` and `{{addvar::A::3}}` is used, the variable `A` will be `8`. `{{addvar::A::B}}` only works when it is in the chat context and it is not the first message.

### `{{calc::A}}`

This will be replaced with the result of the calculation of the provided expression `A`. for example, `{{calc::5+3}}` will be replaced with `8`. You can nest other syntaxes in the expression.

### `{{equal::A::B}}`

This will be replaced with `1` if `A` is equal to `B`, otherwise it will be replaced with `0`.

### `{{not_equal::A::B}}`

> Alias: {{notequal::A::B}}

This will be replaced with `1` if `A` is not equal to `B`, otherwise it will be replaced with `0`.

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

### `{{not::A}}`

This will be replaced with `1` if `A` is `0`, otherwise it will be replaced with `0`.

### `{{startswith::A::B}}`

This will be replaced with `1` if `A` starts with `B`, otherwise it will be replaced with `0`.

### `{{endswith::A::B}}`

This will be replaced with `1` if `A` ends with `B`, otherwise it will be replaced with `0`.

### `{{contains::A::B}}`

This will be replaced with `1` if `A` contains `B`, otherwise it will be replaced with `0`.

### `{{replace::A::B::C}}`

This will be replaced with `A` with all occurrences of `B` replaced with `C`.

### `{{split::A::B}}`

This will be replaced with an array of strings that are separated by `B` in `A`.

### `{{join::A::B}}`

This will be replaced with a string that is created by joining the elements of array `A` with `B`.

### `{{length::A}}`

This will be replaced with the length of `A`. this would not work with arrays.

### `{{array_length::A}}`

> Alias: {{arraylength::A}}

This will be replaced with the length of array `A`. this would not work with strings.

### `{{lower::A}}`

This will be replaced with `A` converted to lowercase.

### `{{upper::A}}`

This will be replaced with `A` converted to uppercase.

### `{{capitalize::A}}`

This will be replaced with `A` with the first letter capitalized.

### `{{round::A}}`

This will be replaced with `A` rounded to the nearest integer.

### `{{trim::A}}`

This will be replaced with `A` with leading and trailing whitespaces removed.

### `{{floor::A}}`

This will be replaced with the largest integer less than or equal to `A`.

### `{{ceil::A}}`

This will be replaced with the smallest integer greater than or equal to `A`.

### `{{abs::A}}`

This will be replaced with the absolute value of `A`.

### `{{pow::A::B}}`

This will be replaced with `A` raised to the power of `B`.

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

### `{{tonumber::A}}`

This would trim all non-numeric characters except for `.`. This doesn't guarantee that the result is a valid number.

### `{{roll::A}}`

> Alias: `{{roll:A}}`

This will be replaced with a random number between 1 and `A`. if `A` starts with `d`, it will be replaced with a random number between 1 and `A` without the `d`.

### `{{spread::A}}`

This will be replaced with a a string created by joining the elements of array `A` with `::` (two colons). This can be used to make multi-parameter syntaxes from arrays. For example, `{{random::{{spread::chicken§pizza§hamburger}}}}` will act same as `{{random::chicken::pizza::hamburger}}`.

### `{{raw::A}}`

This will be replaced with additional asset path data named `A` of the current character.

### `{{img::A}}`

This will be replaced with the image element with the source of the additional asset path data named `A` of the current character.

### `{{audio::A}}`

This will be replaced with the audio element with the source of the additional asset path data named `A` of the current character.

### `{{bg::A}}`

This will be replaced with the background image element with the source of the additional asset path data named `A` of the current character.

### `{{emotion::A}}`

This will be replaced with the image element with the source of the emotion image path data named `A` of the current character.

### `{{asset::A}}`

This will be replaced with the element with the source of the additional asset path data named `A` of the current character. type of the element would be determined by the asset type automatically.

### `{{video::A}}`

This will be replaced with the video element with the source of the additional asset path data named `A` of the current character.

### `{{video-img::A}}`

This will be replaced with the video element with the source of the additional asset path data named `A` of the current character. unlike `{{video::A}}`, the element would be displayed like an image element.

### `{{#if A}}`

This will be replaced with the `content` if `A` is `1`, otherwise it will be replaced with an empty string.

Example:
```
{{#if {{equal::1::1}}}}
Hello Alice!
{{/if}}
```

## Deprecated Syntaxes

Deprecated syntaxes are still supported but are not recommended to use in new projects.

### `<user>`

Works the same as `{{user}}`.
Deprecated due to inconsistency in naming.


### `<bot>`

> Alias: `<char>`

Works the same as `{{char}}`.
Deprecated due to inconsistency in naming.

### `{{main_prompt}}`

> Alias: `{{system_prompt}}`

This will be replaced with the main prompt of the prompt setting.
Deprecated due to incompiatibility with the prompt template system.

### `{{global_note}}`

> Alias: `{{ujb}}`, `{{system_note}}`

This will be replaced with the global_note of the prompt setting.
Deprecated due to incompiatibility with the prompt template system.

### `{{personality}}`

> Alias: `{{char_persona}}`

This will be replaced with the character's personality description.
Deprecated due to deprecation of personality description.

### `{{scenario}}`

This will be replaced with the character's scenario description.
Deprecated due to deprecation of scenario description.


### `{#if A B #}`

This will be replaced with the `content` if `A` is equal to `B`, otherwise it will be replaced with an empty string.
Deprecated due to introduction of blocked `{{#if A}}` syntax.