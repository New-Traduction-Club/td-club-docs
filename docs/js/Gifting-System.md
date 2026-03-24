# Gifting System

The gifting system lets players place `.gift` files in a folder and have Sayori react to them.

## How It Works

The current gifting core is in `game/core/new_gifting_core.rpy`.

`GiftManager` does the following:

* Looks for the gifts folder in this order:
  * `game/gifts/`
  * `<game root>/gifts/`
* Scans files in that folder and checks whether each filename is registered.
* Processes the first registered gift it finds:
  * updates `persistent.js_gift_log[filename]`
  * optionally sets a persistent unlock flag
  * optionally deletes the gift file
  * calls the configured reaction label
* Logs actions to `log/log.txt`.

## Registering a New Gift

In your submod file, register it in an `init` block:

```renpy
init 5 python:
    store.js_gift_manager.register_gift(
        filename="my_awesome_gift.gift",
        reaction_label="my_awesome_gift_reaction",
        delete_after=True,
        unlock_var="my_awesome_gift_unlocked"
    )
```

### `register_gift` Parameters

* `filename` (`str`): Gift filename, including `.gift`.
* `reaction_label` (`str`): Label to call when received.
* `delete_after` (`bool`, optional): Delete file after processing. Defaults to `True`.
* `unlock_var` (`str`, optional): **Name only** of a persistent variable to set on receive.

Important:

* Use `unlock_var="my_flag"`, **not** `unlock_var="persistent.my_flag"`.
* The manager sets `persistent.<unlock_var> = True`.

## Reaction Label Example

```renpy
label my_awesome_gift_reaction:
    s "Oh, wow! A gift for me?"
    s "Thank you so much, [player]!"
    return
```

## Player Flow

The mod's "Look for gifts" topic calls:

```renpy
call check_for_gifts
```

That label triggers `store.js_gift_manager.check_for_gifts()`.

For current built-in gifts, see [Gifts (Spoilers)](./Gifts-(SPOILERS).md).
