# Gifting System

The gifting system allows you to give gifts to Sayori!

## How it Works

The core of the gifting system is the `core/new_gifting_core.rpy` file. It uses a `GiftManager` class to handle all the logic for receiving and processing gifts.

The `GiftManager` scans the `gifts` folder (located in the `game` folder or the root directory) for `.gift` files. When a `.gift` file is found, the system checks if it's a registered gift. If it is, the system calls the corresponding reaction label, deletes the gift file (if configured to do so), and logs that the gift has been received (in `log/log.txt`).

## Adding New Gifts

To add a new gift, you need to create a submod that does the following:

1.  **Create a `.gift` file:** This is an empty file with the `.gift` extension (e.g., `my_awesome_gift.gift`). This file needs to be placed in the `gifts` folder. (Optional but recommended for testing)

2.  **Register the gift:** You need to register your gift with the `GiftManager` so the system knows what to do when it finds your `.gift` file. You can do this by calling the `register_gift` function in an `init` block in your submod's `.rpy` file.

Here's an example of how to register a gift:

```renpy
init python:
    store.js_gift_manager.register_gift(
        filename="my_awesome_gift.gift",
        reaction_label="my_awesome_gift_reaction",
        delete_after=True,
        unlock_var="persistent.my_awesome_gift_unlocked"
    )
```

### `register_gift` Parameters

*   `filename` (str): The name of the gift file (e.g., `"my_awesome_gift.gift"`).
*   `reaction_label` (str): The label to call when the gift is found.
*   `delete_after` (bool): If `True`, the gift file will be deleted after being received.
*   `unlock_var` (str, optional): A persistent variable to be set to `True` after receiving the gift. This is useful for unlocking new content or features.

3.  **Create the reaction label:** This is the Ren'Py label that will be called when the gift is received. In this label, you can define Sayori's reaction to the gift.

Here's an example of a reaction label:

```renpy
label my_awesome_gift_reaction:
    s "Oh, wow! A gift for me?"
    s "Thank you so much, [player]!"
    return
```
