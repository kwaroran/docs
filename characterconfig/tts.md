# TTS

TTS (Text to speech) makes character's response to a speech. the TTS settings (excluding API keys) are embeded to the character, making shared characters to have the same TTS settings.

## Providers

These are the TTS providers that are supported by RisuAI. Some of them requires an API key to use, and you must provide the API key in [Other Bots](/characterconfig/otherbots) settings.

### Web Speech

Web Speech is the most accessible TTS, which is provided by the browser. It is supported by most of the modern browsers. It is free, and doesn't require any API key. However, it has some limitations:
- It doesn't support all the languages.
- The voice quality is not good.
- Voice varys between the browsers.

### ElevenLabs

ElevenLabs is a TTS provider that provides high quality voices. It requires an API key to use. It supports many languages, and has high quality voices, however, its expensive. You can get the API key from [ElevenLabs](https://elevenlabs.io/)

### OpenAI

OpenAI also provides TTS service. It requires an API key to use. However, OpenAI's TTS is not as good, since:
- The variety of voices are very limited.
- Customization is limited.

However, If you already have an OpenAI API key, you can just simply use it for the TTS too, making it easier to use.

### NovelAI

NovelAI also provides TTS service. It requires an API key to use. you can also use custom voice seed, which would make the voice more unique. To get a NovelAI API key, see [NovelAI API Key Guide](/guides/novelaiapi)

### Hugging Face

Hugging Face also provides TTS service. It requires an API key to use. It has many voices, and supports many languages. To get a Hugging Face API key, see [Hugging Face API Key Guide](/guides/huggingfaceapi)

### VITS

You can use your own VITS model to generate the TTS, directly in the client, without any API key. to setup, first, get a VITS model, in hugging face format, and zip it as `model.zip`. then, upload the model pressing `Select Model` button.

VITS models are embeded to the character, making shared characters to have the same VITS model.