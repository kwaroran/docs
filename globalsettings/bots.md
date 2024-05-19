# Chat Bot

On chat bot tab you can set the bot settings. like provider, prompt settings, and other.
There is simple settings mode and advanced settings mode, which can be toggled by the switch on top of the page.

## Simple Settings

On simple settings mode, there are only few settings that you can set, and the client would handle the rest.

 - Model: AI model that would be used for the chat. You can select the model that you want to use for the chat.
 - API Key: API key that would be used for the chat. Some of the models requires an API key to use.

For getting an API key, see [API Key Guide](/guides/apikey)

## Advanced Settings

On advanced settings mode, you can configure powerful settings. however, for beginners, it is recommended to keep the simple settings, unless you know what you are doing.

Only a few Provider specific settings are available in this document for now. More will be added later.

### Models

There are two types of models that you should set on the advanced settings.

- Model: AI model that would be used for the chat.
- Auxiliary Model: Auxiliary model that would be used for non-chat purposes, like summarization, emotion detection, etc.

We recommend to keep the auxiliary model to cheap model, since it would be used for non-chat purposes, and it would be more cost-effective. or if you just do not want to care about it, you can just keep it same as the model.

### API Key

API key that would be used for the chat, like the simple settings. for getting an API key, see [API Key Guide](/guides/apikey).

### Max Context Size

The maximum context size of the AI in tokens. More context would mean AI's more memory, but it would also mean more cost. AI models have hard limit of context size, and if the context size is too big, the AI might throw an error.

### Temperature

Temperature is the setting that would control the randomness of the AI's response. The higher the temperature, the more creative the AI would be, but it would also be more chaotic. The lower the temperature, the more predictable the AI would be, but it would also be more boring.

### Top P

Top P is the setting that would control the diversity of the AI's response. The higher the Top P, the more diverse the AI would be, but it would also be more chaotic. The lower the Top P, the more predictable the AI would be, but it would also be more boring.

### Top K

Top K is the setting that would control the diversity of the AI's response. Unlike Top P, Top K would only consider the top K tokens, and would ignore the tokens that are not in top K. Less Top K would make the AI to be more boring, but more accurate.

If Top K is set to 0, it would be disabled.

### Min P

Min P is the setting that would control the diversity of the AI's response. Unlike Top K, Min P uses the probability of the tokens, and would ignore the tokens that are below the Min P. Less Min P would make the AI to be more creative, but more chaotic and vice versa for more Min P.

### Top A

Top A is the setting that would control the diversity of the AI's response. Unlike Top K, Top A would only consider the top A tokens, and would ignore the tokens that are not in top A.

### Repetition penalty

Repetition penalty is the setting that would control the repetition of the AI's response. The higher the repetition penalty, the less the AI would repeat itself, but it would also be more chaotic. The lower the repetition penalty, the more the AI would repeat itself, but it would also be more boring.

This setting only applies when model does not support Frequency Penalty and Presence Penalty.

### Frequency penalty

Frequency penalty is the setting that would control the repetition of the AI's response. The higher the frequency penalty, the less the AI would repeat itself, but it would also be more chaotic. The lower the frequency penalty, the more the AI would repeat itself, but it would also be more boring. The frequency penalty only applies to the tokens that are already in the context.

### Presence penalty

Presence penalty is the setting that would control the repetition of the AI's response. The higher the presence penalty, the less the AI would repeat itself, but it would also be more chaotic. The lower the presence penalty, the more the AI would repeat itself, but it would also be more boring. The presence penalty only applies to the tokens that are only in the AI's response.

### Auto Suggest 

Auto suggest is a prompt that would be sent to the AI model if "Auto Suggest" is enabled. The AI model would generate the response based on the prompt, and the response would be shown to the user as a suggestion. The user can select the suggestion by clicking on it.

### Bias

Bias is the setting that would control the AI's response. The bias would be added to the AI's response, and it would make the AI to generate the response less or more. The bias can be positive or negative, and it can be a number between -101 and 100. The higher the bias, the more the AI would generate the response, and the lower the bias, the less the AI would generate the response.

If the bias is set to -101, it would work as "super ban", and RisuAI would try to avoid generating the response.

### Main Prompt 

Main prompt is the prompt that would be sent to the AI model. Put main instructions here. main prompt as independent field would be hidden if prompt template setting is enabled.

### Jailbreak Prompt 

Jailbreak prompt is the prompt that would be sent to the AI model. Put jailbreak instructions here. jailbreak prompt as independent field would be hidden if prompt template setting is enabled.

### Global Note 

Global note is the prompt that would be sent to the AI model. Put important information here. global note as independent field would be hidden if prompt template setting is enabled.

### Formating Order 

Formating order is the order of the formating. The formating would be applied in the order of the formating order. formating order would be hidden if prompt template setting is enabled.

### Prompt Template

See [Prompt Template](/globalsettings/prompttemplate) for more information.
