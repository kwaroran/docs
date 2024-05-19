# Character Display

On Character Display tab you can set the character icon and additional character screen settings.

## Character Icon

On Character Icon section you can set the character icon. The character icon is the image that would be shown on the chat window. By default, the character icon is 1:1 aspect ratio, but you can change to 2:3 aspect ratio by checking the "Protrait" checkbox.

## Additional Character Screen

Additional Character Screen is where you can put character's image on additional screen or inlay.

### Modes

There are two modes for Additional Character Screen. "Emotion Image" and "Image Generation".

#### Emotion Image

If you set the mode to Emotion Images, the character image would be shown next to the text window.
the character image would change dynamicly, depending on the conversation.

How the emotion image works is, you can set it at the [Emotion Image tab at the global settings.](/globalsettings/otherbots#emotion-image)

You can add character images on bottom of the emotion image menu. the image must have a emotion name. the emotion name is used on choosing the image, so write it carefuly.

if the emotion name is `neutral`, it would be set as default image.

#### Image Generation

If you set the mode to Emotion Images, the ai-generated image would be shown next to the text window.
the character image would be generated every time, depending on the conversation.
To use it, you must set up the image generation settings to work. image generation settings is on the other bot tab, on the global settings.

Image Generation Prompt is the prompt for image generation. `{​{slot}​}` would be replaced with ai's response,
Image Generation Negative Prompt is the prompt for image generation. `{​{slot}​}` does nothing here, and 
Image Generation Instructions is a prompt which would sent to ai to generate `{​{slot}​}` for Image Generation Prompt.

### Inlay Screen

If you turn on Inlay Screen checkbox, the images would be put in screen. and this would make ai to select or generate image at the same time when they generate, which can make the result more accurate.