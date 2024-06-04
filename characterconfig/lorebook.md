# Lorebook

Lorebooks are collection of lore entries. Each entry is a piece of prompt that would be sent to the AI model. unlike character description, lore entries can use advanced conditions, mainly activation by keywords.

Lorebooks can be embeded to characters, or chats, or even modules.

## Structure

![](/static/lorebook.png)

### Name

The name of the lorebook. This is used to identify the lorebook in the character configuration. this doesn't effect the AI's response, just for identification.

### Activation Keys

Activation keys are the keywords that would activate the lore entry. The AI would only respond to the lore entry if the activation keys are present in the chat messages. The activation keys are separated by commas.

### Insertion Order 

The order of the lore entries in the lorebook. If the order is higher, the lore entry would be inserted more later in the context, which would make the AI to consider the lore entry more important. It would also effect the removal of the lore entry if the lore entry is too much. in that case, the lore entries with lower order would be removed first.

### Prompt

The prompt that would be sent to the AI model. If the lore entry is activated, this prompt would be sent to the AI model to generate the response.

### Always Active

If this is enabled, the lore entry would be always active, regardless of the activation keys. This is useful for the lore entries that should be always active.

### Selective

If this is enabled, the secondary activation keys would appear, and it would also require the secondary activation keys to activate the lore entry.

### Use Probability Condition

If this is enabled, the lore entry would only be activated on certain probability. This is useful for the lore entries that should be activated randomly.

## Settings

![](/static/lore_settings.png)

### Recursive Scanning

If this is enabled, the AI would also scan the lore entries' prompts for the activation keys.

### Full Word Matching

If this is enabled, the AI would only consider the activation keys if they are full words. for example, if the activation key is `cat`, the AI would only consider the activation key if the word is `cat`, not `caterpillar`.

### Lorebook Search Depth

The depth of the lorebook search. The AI would only consider only recent `<Lorebook Search Depth>` chats for the activation keys. We recommend to keep this value by default, if you don't know what you are doing.

### Lorebook Max Tokens

The maximum tokens that the all lore entries' prompts can have. If the lore entries' prompts have more tokens than this value, the lore entries would be removed, starting from the lore entries with lower [Insertion Order](#insertion-order).

## Decorators

Decorators are advanced conditions, or effects that can be applied to the lore entries. The decorators should be provided at the [Prompt](#prompt) field, and should be started with `@@`.

Example:

```
@@depth 0

This is the prompt
```

### @@depth N

If this decorator is provided, the AI would put the response of the lore entry at the depth of N. This is useful for the lore entries that should be considered more important.

### @@activate_only_after N

If this decorator is provided, the AI would only activate the lore entry after the Nth chat message. This is useful for the lore entries that should be activated after certain conditions.

### @@activate_only_every N

If this decorator is provided, the AI would only activate the lore entry every Nth chat message. This is useful for the lore entries that should be activated periodically.

### @@reverse_depth N

If this decorator is provided, the AI would put the response of the lore entry at the reverse depth of N. This is useful for the lore entries that should be considered less important.

### @@role A

If this decorator is provided, the AI would consider the lore entry as the role of A. This is useful for the lore entries that should be considered as the role of A. roles can be `user`, `system` or `assistant`.

### @@scan_depth A

If this decorator is provided, the AI would scan the lore entry for the activation keys at the depth of A, regardless of the [Lorebook Search Depth](#lorebook-search-depth). This is useful for the lore entries that should be activated at the certain depth.

### @@is_greeting N

If this decorator is provided, the AI would consider the lore entry as the greeting of index N.

### @@position A

If this decorator is provided, the AI would consider the lore entry as the position of A. positions can be `personality`, `scenario` or `pt_<name>`. `pt_<name>` is the position of that is provided in prompt template.

### @@ignore_on_max_context

If this decorator is provided, the AI would ignore the lore entry if the context is full.

### @@additional_keys A,B,C...

If this decorator is provided, the AI would consider the lore entry as additional keys of A, and it would also require one of the additional keys to activate the lore entry.

### @@exclude_keys A,B,C...

If this decorator is provided, the AI would consider the lore entry as exclude keys of A, and it would not activate the lore entry if one of the excluded keys is present.

### @@probability N

If this decorator is provided, the AI would only be activated on the probability of N%. This is useful for the lore entries that should be activated randomly.

### @@activate

If this decorator is provided, the AI would activate the lore entry, regardless of all other conditions.

### @@dont_activate

If this decorator is provided, the AI would not activate the lore entry, regardless of all other conditions.