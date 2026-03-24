# Submod API Reference

This page documents the public integration points currently used by submods.

---

## Submod registration metadata

Source: `game/additional/zz_submods.rpy`

Use this to show your submod in the in-game Submods menu.

```renpy
init -991 python in fae_extras:
    Extras(
        name="My Submod",
        creator="YourName",
        description="What this submod does."
    )
```

### API

* `Extras(name, creator, description)`
* `isInstalled(name)` -> `bool`

---

## Gifting API

Source: `game/core/new_gifting_core.rpy`

Global manager:

* `store.js_gift_manager`

### Register a gift

```renpy
init 5 python:
    store.js_gift_manager.register_gift(
        filename="my_item.gift",
        reaction_label="reaction_my_item",
        delete_after=True,
        unlock_var="my_item_unlocked"
    )
```

### Methods

* `register_gift(filename, reaction_label, delete_after=True, unlock_var=None)`
* `check_for_gifts()`
* `get_gift_count(filename)` -> `int`

### Notes

* `unlock_var` is the variable name only.  
  Example: `unlock_var="my_item_unlocked"` sets `persistent.my_item_unlocked = True`.
* Gift scan directories: `game/gifts/`, then `<root>/gifts/`.

---

## Rooms / backgrounds API

Source: `game/additional/bgs.rpy`

Namespace:

* `store.fae_rooms`

### Register a room

```renpy
init 5 python:
    import store.fae_rooms as fr
    fr.register_room(
        "my_room",
        "my_room",
        display_name=_("My Room")
    )
```

### API

* `register_room(id, image_directory, **kwargs)`

Common kwargs:

* `display_name` (required in practice by `Rooms`)
* `decoration_permitted`
* `when_enter`
* `when_leave`

Required files:

* `mod_assets/rooms/<image_directory>/<id>-day.png`
* `mod_assets/rooms/<image_directory>/<id>-night.png`

---

## Minigame Hub API

Source: `game/core/mg_core.rpy`

### Register minigame

```renpy
init 10 python:
    register_minigame(
        label="my_minigame_label",
        name=_("My Minigame"),
        image="mod_assets/images/minigames/covers/my_cover.png",
        unlocked=True,
        condition=None,
        description=_("Optional description"),
        prep=None,
        pid="my_minigame_unique_id"
    )
```

### API

* `register_minigame(label, name, image, unlocked=True, condition=None, description=None, prep=None, pid=None)`
* `get_registered_minigames(only_unlocked=True)`
* `import_legacy_minigames(as_cover=...)`

Notes:

* `unlocked` can be bool or callable.
* `condition` can be callable or expression string.
* The hub entry point label is `mg_hub`.

---

## Outfits API

Source: `game/core/new_outfits.rpy`

Namespace:

* `store.fae_outfits`

### Public helpers

* `_m1_new_outfits__register_wearable(wearable)`
* `_m1_new_outfits__register_outfit(outfit, player_created=False)`
* `get_wearable(reference_name)`
* `get_outfit(reference_name)`
* `get_all_wearables()`
* `get_all_outfits()`

### Wearable classes

* `FAEHairstyle`
* `FAEEyewear`
* `FAEAccessory`
* `FAEClothes`
* `FAEHeadgear`
* `FAENecklace`

### Example

```renpy
init 5 python:
    import store.fae_outfits as fo

    fo._m1_new_outfits__register_wearable(
        fo.FAEAccessory(
            reference_name="myauthor_pin",
            display_name="Cute Pin",
            unlocked=True,
            is_fae_wearable=False,
            author="MyAuthor"
        )
    )
```

---

## Dialogue registration API

Source: `game/dialogs/handler.rpy`

Most topic-style submods should use `Chat` + `chatReg`.

```renpy
init 5 python:
    chatReg(
        Chat(
            persistent._chat_db,
            label="s_topics_my_topic",
            unlocked=True,
            prompt=__("My Topic"),
            random=True,
            category=[__("Misc")]
        ),
        chat_group=CHAT_GROUP_NORMAL
    )
```

Important:

* `label` must exist.
* Use `chat_group` constants (for example `CHAT_GROUP_NORMAL`).
