## Additional Character Screen

![](/static/chardis.png)

Additional Character Screen is where you can put character's image on additional screen or inlay.

### Modes

There are two modes for Additional Character Screen. "Emotion Image" and "Image Generation".

#### Emotion Image

If you set the mode to Emotion Images, the character image would be shown next to the text window.
the character image would change dynamicly, depending on the conversation.

You can add character images on bottom of the emotion image menu. the image must have a emotion name. the emotion name is used on choosing the image, so write it carefuly.

if the emotion name is `neutral`, it would be set as default image.

#### Image Generation

If you set the mode to Emotion Images, the ai-generated image would be shown next to the text window.
the character image would be generated every time, depending on the conversation.
To use it, you must set up the image generation settings to work. image generation settings is on the other bot tab, on the global settings.

Image Generation Prompt is the prompt for image generation. `{​{slot}​}` would be replaced with ai's response,
Image Generation Negative Prompt is the prompt for image generation. `{​{slot}​}` does nothing here, and 
Image Generation Instructions is a prompt which would sent to ai to generate `{​{slot}​}` for Image Generation Prompt.

#### Inlay Screen

If you turn on Inlay Screen checkbox, the images would be put in screen. and this would make ai to select or generate image at the same time when they generate, which can make the result more accurate.