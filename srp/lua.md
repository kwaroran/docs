# Trigger Script (Lua Mode)

On trigger script lua mode, you can write a lua script to handle the trigger event. The script will be executed when the trigger event is triggered.

## Callback Function

There are three normal callback functions you can use in the lua script:
- `onStart(triggerId)`: This function will be called when chat is sent.
- `onOutput(triggerId)`: This function will be called when AI response is received.
- `onInput(triggerId)`: This function will be called when user input is received.

For button events (like `{{button::Display::TriggerName}}`), it calls the function with same name as TriggerName.

You can also use `listenEdit(type, callback)` to listen for edit events. The type can be `editRequest`, `editDisplay`, `editInput`, and `editOutput`. The callback function will be `callback(triggerId, data)`.


### Example

```lua
function onInput(triggerId)
    alertNormal(triggerId, "input received!")
end
```

The above script will make an alert with the message `input received!` when user input is received.

```lua
listenEdit("editDisplay", function(triggerId, data)
    local prefix = getState(triggerId, "prefix") or ""
    return prefix .. data
end)
```

The above script will append prefix from the state variable to the display message.

```lua
function onButton(triggerId)
    alertNormal(triggerId, "button clicked!")
end
```

The above script will make an alert with the message `button clicked!` when the button `{{button::Display::onButton}}` is clicked.

## Functions

You can use the following functions in the lua script. Every function except `log` must be called with the `triggerId` as the first argument for security reasons. you can get the `triggerId` from the callback function.

All functions except `setChatVar`, `getChatVar`, `setState`, `getState`, `log` would not work in editDisplay event.

### `log(message)`

Log the message to the console. unlike `print`, this outputs as a JSON format, making arrays and objects display correctly in the devtools console.

### `setChatVar(triggerId, key, value)`

Set a chat variable with the key and value. value must be a string.

### `getChatVar(triggerId, key)`

Get the value of a chat variable with the key.

### `setState(triggerId, key, value)`

Set a state variable with the key and value. value must be a JSON serializable. (like string, number, boolean, array, object)

### `getState(triggerId, key)`

Get the value of a state variable with the key.

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

### `getName(triggerId)`

Returns the name of the current character.

### `setName(triggerId, name)`

Set the name of the current character.

### `getDescription(triggerId)`

Returns the description of the current character.

### `setDescription(triggerId, description)`

Set the description of the current character.

### `getCharacterFirstMessage(triggerId)`

Returns the first message of the current character.

### `setCharacterFirstMessage(triggerId, message)`

Set the first message of the current character.

### `getBackgroundEmbedding(triggerId)`

Returns the background embedding of the current character.

### `setBackgroundEmbedding(triggerId, embedding)`

Set the background embedding of the current character.

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


## Tips

- If you do not know how to write a lua script, you can refer to the [lua manual](https://www.lua.org/manual/5.4/) or ask for help to the AI chatbot like RisuAI chat playground.
- Since the application only offers a small GUI for the lua script, we recommend using an external editor like [VSCode](https://code.visualstudio.com/) for writing the script, and then copy and paste it to the application.
- We recommend using `log` instead of `alert` or `print` for debugging, as it will not disturb other functions, and displays the data in a more readable format.
- We recommend using `setState` and `getState` to store data more than `setChatVar` and `getChatVar`, as it supports more data types.
- Every time the trigger event is triggered, the lua script will be executed from the beginning. So if you want to keep some data, you must use chat variables or state variables.
- [json.lua](https://github.com/rxi/json.lua) is included in the lua environment, so you can use `json.encode` and `json.decode` to serialize and deserialize JSON data.
- The lua script is executed in a sandbox environment, so you can't access the file system or network.
- You can't use external libraries except the included `json.lua`.
- If error occurs in the lua script, the application will work as if the script is not executed, and the error message will be displayed in the console.