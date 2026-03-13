# CODING STYLE

These are the coding conventions you should follow when creating dialogue for Sayori.

## INDENTS

Indents are **4** spaces. No more, no less.

## LABELS

Label names should be all lowercase, with words separated by underscores.

E.G. `s_topics_example`

Specific prefixes are reserved for certain things and help organize the code:

- `s_topics_`: Used for general random topics.
- `s_answer_`: Used for player-initiated questions about specific subjects.
- `compliment_`: Used for compliments.
- `greeting_`: Used for regular greetings.
- `event_`: Used for special events.
- `s_farewell_`: Used for farewells.

There *are* more, so be careful to check existing files if you are unsure.

## PERSISTENT

Persistent data is a way to store information that saves even when the game closes. You should only use this if you need to remember a variable's value across different play sessions (for example, tracking if a topic has been seen before).

## VARIABLES

Variable names should be descriptive and use `lowercase_with_underscores`. Abbreviations are fine if they are clear.

## COMMENTS

Make sure to comment your code!

Despite python being readable by definition, comments help us understand why we doing something or that the effects of doing something is helpful.

## ASSETS

Any custom files (images, music, etc.) must go in the `game/mod_assets/` folder. If you have multiple assets, please group them in a descriptive subfolder.


# DIALOGUE

To add new dialogue, you must register it using a `chatReg` block inside an `init python` block.

Below is an example of a dialogue block:

```renpy

init 5 python:

    chatReg(
        Chat(
            persistent._chat_db,
            label="s_topics_example",
            unlocked=True,
            prompt="Example topic",
            random=True,
            category=["Misc", "Examples"]
        ),
        chat_group=CHAT_GROUP_NORMAL
    )


label s_topics_example:

    s abhfbaoa "This is an example topic."
    s abhfbboa "I don't think this actually belongs here though."
    s abhfbloa "Who even thought of this?"
    s abhfbaoa "They really shouldn't be allowed to contribute."

    return
```

## DIALOGUE TIPS

- The `label` in `Chat()` must exactly match the `label` name in your script (e.g., `label="s_topics_example"` matches `label s_topics_example:`).
- Categories use a capital letter for the first word only (e.g., `["My category", "Another one"]`).
- Categories are a list, so you can make your topic appear in multiple menus.
- Set `random=True` if you want the topic to appear randomly during conversation.
- Set `random=False` if you want the player to have to select it from the "Talk" menu.