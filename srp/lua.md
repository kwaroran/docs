# Trigger Script (Lua Mode)

On trigger script lua mode, you can write a lua script to handle the trigger event. The script will be executed when the trigger event is triggered.

## Callback Function

There are three normal callback functions you can use in the lua script:
- `onStart(triggerId)`: This function will be called when chat is sent.
- `onOutput(triggerId)`: This function will be called when AI response is received.
- `onInput(triggerId)`: This function will be called when user input is received.

For button events (like `{{button::Display::TriggerName}}`), it calls the function with same name as TriggerName.

### Example

```lua
function onStart(triggerId)
    print("onStart: " .. triggerId)
end

function onOutput(triggerId)
    print("onOutput: " .. triggerId)
end

function onInput(triggerId)
    print("onInput: " .. triggerId)
end

function buttonClick(triggerId)
    print("buttonClick: " .. triggerId)
end
```

The above script will print the triggerId when the corresponding callback function is called, and also print `buttonClick: triggerId` when the button `{{button::buttonname::buttonClick}}` is clicked.

You can also use `listenEdit(type, callback)` to listen for edit events. The type can be `editRequest`, `editDisplay`, `editInput`, and `editOutput`. The callback function will be `callback(triggerId, data)`.

## Functions

You can use the following functions in the lua script. however, all functions except `setChatVar` and `getChatVar` do not work on `editDisplay` event.

### `setChatVar(triggerId, key, value)`

Set a chat variable with the key and value.

### `getChatVar(triggerId, key)`

Get the value of a chat variable with the key.

### `stopChat(triggerId)`

Stop the chat. this only works on some trigger events.

### `alertError(triggerId, message)`

Show an error alert with the message.

### `alertNormal(triggerId, message)`

Show a normal alert with the message.

### `alertInput(triggerId, message)`

Show an input alert with the message, and return the input value.

### `setChat(triggerId, index, message)`

Set the chat message at the index. index starts from 0.

### `setChatRole(triggerId, index, role)`

Set the chat role at the index. index starts from 0. role can be `user` and `char`.

### `cutChat(triggerId, start, end)`

Cut the chat message from start to end. start and end are both 0-based index.
to cut only one message, use `removeChat(triggerId, index)`.

### `removeChat(triggerId, index)`

Remove the chat message at the index. index starts from 0.

### `addChat(triggerId, role, message)`

Add a chat message with the message and role. role can be `user` and `char`.

### `insertChat(triggerId, index, role, message)`

Insert a chat message at the index with the message and role. index starts from 0. role can be `user` and `char`.

### `removeChat(triggerId, index)`

Remove the chat message at the index. index starts from 0.

### `getChatLength(triggerId)`

Get the chat length.

### `getFullChat(triggerId)`

Get the full chat message, with the format of:
```lua
{
    {role = "user", data = "user message"},
    {role = "char", data = "char message"},
    ...
}
```

### `setFullChat(triggerId, chat)`

Set the full chat message, with the format of:
```lua
{
    {role = "user", data = "user message"},
    {role = "char", data = "char message"},
    ...
}
```

### `similarity(triggerId, source, value)`

> This function requires low level access.

Perform a similarity sort between the source and value.
source must be a array of strings, and value must be a string.
return a array of index sorted by similarity.

This is a async function. use `similarity(triggerId, source, value):await()` to wait for the result.

### `generateImage(triggerId, prompt, negative)`

> This function requires low level access.

Generate an image with the prompt and negative. returns the asset CBS (like `{{asset::assetId}}`).

This is a async function. use `generateImage(triggerId, prompt, negative):await()` to wait for the result.

### `LLM(triggerId, data)`

> This function requires low level access.

Performs a llm request with the data. returns the response.

data must be a message format, with the format of:
```lua
{
    -- the message role, can be "system", "assistant", "user"
    {
        role = "system",
        data = "system message"
    },
    {
        role = "assistant",
        data = "char message"
    },
    {
        role = "user",
        data = "user message"
    }
    ...
}
```

the response format is:

```lua
{
    success = true,
    message = "response message",
}
```

This is a async function. use `LLM(triggerId, data):await()` to wait for the result.

### `simpleLLM(triggerId, message)`

> This function requires low level access.

Performs a simple llm request with the message. returns the response.
both the message and response format is string.

This is a async function. use `simpleLLM(triggerId, message):await()` to wait for the result.