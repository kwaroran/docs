# Advanced Settings

In Advanced Settings, you can configure powerful settings. however, for beginners, it is recommended to keep the default settings, since it can cause unexpected results.

## Example Message 

Example messages are the messages that would be sent to the AI model to generate the response.
These example message would be provided to the AI model until the context is full.

Here are example-example messages, for character named Haruhi.
```
<START>
{{user}}: hi, how are you?
{{char}}: I'm doing great!
<START>
{{user}}: hi, how are you?
{{char}}: I'm eating {{random::apple,banana,orange}}.
```

`<START>` marks the start of the example message, and `{{user}}` and `{{char}}` marks the speaker of the message.

## Creator's Comment 

Creator's comment is the comment, that would be shown on top of the chat, and not sent to the AI model. This is useful for the creators to provide information about the character.

creator's comment can be written in markdown format, and you can use creator's comment for each language.

## System Prompt

System prompt is the prompt that would be added as a "Main Prompt". However, we DO NOT recommend to use this, since it can cause unexpected results. use [Lorebook](/characterconfig/lorebook) instead for this purpose.

## Global Note Replacement 

Global note replacement is the prompt that would be replace "Global Note". However, we DO NOT recommend to use this, since it can cause unexpected results. use [Lorebook](/characterconfig/lorebook) with `@@end` decorator instead for this purpose.

## Additional Description 

Additional description is the description that would only be added to the character's description if recent chat's similarity is higher than certain value. the similarity is calculated by the AI model which runs in the client.

Each prompt should be separated by two new lines.

## SupaMemory

The SupaMemory section displays current SupaMemory data. You can view and edit the SupaMemory data here. do not edit the SupaMemory data unless you know what you are doing.

## Background Embedding 

Background embedding is the setting that would embed the background to the chat. It allows [HTML tags](/syntax/html) and [Curly Braced Syntaxes](/syntax/cbs_memo) to be used in the background.

## Creator
Creator field allows you to set the creator of the character. This is useful for the creators to provide information about the character.

## Character Version
Character version is the version of the character. This is useful for the creators to provide information about the character.

## Depth Prompt
Depth prompt is the prompt that would added in certain depth. the lower the depth, the more important the prompt would be.

## Alternative First Messages

Alternative first messages is just like it sounds, a [First Message](/characterconfig/basic#first-message) which can be selected by the user. if alternative first messages are provided, the user can select the first message by arrow buttons on the first message.

## Utility Bot

If Utility bot field is checked, the character would be considered as a utility bot, which would ignore ALL OF THE GLOBAL PROMPT SETTINGS. This is useful for the characters that should be used as utility bots, or characters that only works well on certain prompts.