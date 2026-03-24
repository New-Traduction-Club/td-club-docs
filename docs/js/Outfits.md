# Custom Outfits & Wearables

This guide explains how to add custom outfits, wearables, and reactions for Sayori.

## Prefixes and Naming

To avoid collisions between submods, prefix your `reference_name` with something unique to you (for example: `myauthor_cool_shirt`).

Reserved namespaces:

* `fae_` is used by built-in content.
* `js_` is reserved for new mod content.

For JSON-loaded wearables, names starting with `fae_` are rejected by the loader.

## Two Supported Workflows

* **JSON workflow (`.json`)**: easiest for static content.
* **Code workflow (`.rpy`)**: better when you need custom logic.

---

## JSON Workflow

### Wearable definition file

Create a file in:

`game/mod_assets/sayori/sitting/jsons/`

Required keys:

* `reference_name`
* `display_name`
* `unlocked`
* `category` (`hairstyle`, `eyewear`, `accessory`, `clothes`, `headgear`, `necklace`)

Optional key:

* `author`

Example:

```json
{
    "reference_name": "myauthor_headphones",
    "display_name": "Cool Headphones",
    "unlocked": true,
    "category": "accessory",
    "author": "MyAuthor"
}
```

### Outfit definition file

Also in:

`game/mod_assets/sayori/sitting/jsons/`

Required keys:

* `reference_name`
* `display_name`
* `unlocked`
* `clothes`
* `hairstyle`

Optional keys:

* `eyewear`
* `accessory`
* `headgear`
* `necklace`

Example:

```json
{
    "reference_name": "myauthor_test_outfit",
    "display_name": "MyAuthor's Example Outfit",
    "unlocked": true,
    "clothes": "fae_hoodie",
    "hairstyle": "fae_bow",
    "accessory": "myauthor_headphones"
}
```

### Asset structure

All assets are under `game/mod_assets/sayori/sitting/`.

Minimum expectations by category:

* `clothes`:
  * `body/<reference_name>/1.png`
  * `arms/<reference_name>/back-arm.png`
  * arm pose files (for example `folded.png`, `left-index-point.png`, etc.)
  * `backarms/<reference_name>/...` files for supported back-arm states
* `hairstyle`:
  * `hair/<reference_name>/a.png`
* `accessory`, `eyewear`, `headgear`, `necklace`:
  * `<category>/<reference_name>/sitting.png`

---

## Code Workflow (`.rpy`)

Create a submod file (for example `game/submods/myauthor_cool_outfit.rpy`) and register content in `init 5 python`.

```python
init 5 python:
    import store.fae_outfits as fae_outfits

    fae_outfits._m1_new_outfits__register_wearable(
        fae_outfits.FAEClothes(
            reference_name="myauthor_cool_shirt",
            display_name="Cool T-Shirt",
            unlocked=True,
            is_fae_wearable=False,
            author="MyAuthor"
        )
    )

    fae_outfits._m1_new_outfits__register_wearable(
        fae_outfits.FAEHairstyle(
            reference_name="myauthor_spiky_hair",
            display_name="Spiky Hair",
            unlocked=True,
            is_fae_wearable=False,
            author="MyAuthor"
        )
    )

    fae_outfits._m1_new_outfits__register_outfit(
        fae_outfits.FAEOutfit(
            reference_name="myauthor_rocker_style",
            display_name="Rocker Style",
            unlocked=True,
            is_fae_outfit=False,
            clothes=fae_outfits.get_wearable("myauthor_cool_shirt"),
            hairstyle=fae_outfits.get_wearable("myauthor_spiky_hair")
        )
    )
```

About unlock logic:

* `unlocked` on wearables/outfits is currently stored as a value.
* If you need conditions, evaluate them in your own code first and pass the resulting boolean.

---

## Outfit Reactions

When changing clothes from the outfit UI, the game checks for:

`reaction_<category>_<reference_name>`

Example:

```renpy
label reaction_clothes_myauthor_cool_shirt:
    s "Oh, this T-shirt is so cool! I feel like a rock star."
    s "Thanks for picking it out for me, [player]!"
    return
```

If the label exists, it is called automatically. If not, no reaction is shown.
