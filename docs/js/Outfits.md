# Custom Outfits & Wearables

This guide explains how to add custom outfits, wearables, and reactions for Sayori.

**A Note on Prefixes:** To prevent conflicts between different submods, it is highly recommended to prefix your `reference_name`s with a unique identifier, like your author name (e.g., `myauthor_cool_shirt`). The prefix `fae_` is used by the base mod and should not be used. The `js_` prefix is reserved for new official content.

There are two methods for adding new clothing and outfits:
-   **Simple Method (`.json` files):** It's quick, safe, and requires no programming knowledge.
-   **Advanced Method (`.rpy` files):** Ideal for submods with complex logic. It offers complete control over the properties and unlock conditions of a wearable.

## Choosing Your Method: `.json` vs. `.rpy`

| Feature | Simple Method (`.json`) | Advanced Method (`.rpy`) |
| :--- | :--- | :--- |
| **Ease of Use** | Very easy. Fill out a text file. | Intermediate. Requires basic Python/Ren'Py knowledge. |
| **Flexibility** | Limited. You can only define static properties. | Total. Full control to program logic and dynamic properties. |
| **Conditional Logic** | None. An item is either unlocked or not from the start. | Fully supported. Unlock items based on affection, events, date, etc. |
| **Risk of Errors** | Low. A typo might prevent one item from loading, but won't crash the game. Note: In Android the typo errors in json will crash the game. | High. A syntax error can prevent the game from starting. |
| **Use Case** | Simple clothing additions. | To integrate clothing with gameplay mechanics. |

---

## Simple Method: Using `.json` Files

This method involves creating `.json` definition files for your assets. It's the best way to add simple clothing that is available immediately.

### 1. Making New Wearables

A "wearable" is any single item of clothing Sayori can wear in one of her 'slots'.

Any piece of custom clothing has two portions:
- **Wearable definition**: A single `.json` file that describes the clothing so it can be registered and loaded in the game.
- **Wearable assets**: The `.png` files containing the graphics for the item.

#### Wearable Definition File

The definition file is a `.json` file that describes a piece of clothing. It **must** be placed in the `game/mod_assets/sayori/sitting/jsons/` directory.

The file **must** include:

- `reference_name`: A unique internal name for the clothing (e.g., `myauthor_cool_shirt`). This **cannot** use the `fae_` or `js_` prefixes and must not be changed after release.
- `display_name`: The name for the clothing that appears in-game.
- `unlocked`: Whether this clothing is unlocked by default. This should almost always be `true`.
- `category`: Defines what slot the clothing uses. It **must** be one of the following:
    - `hairstyle`
    - `eyewear`
    - `accessory`
    - `clothes`
    - `headgear`
    - `necklace`
- `author` (Optional): Your name, or the name of the artist.

**The `.json` filename must be the same as its `reference_name`**. For example, a wearable with `reference_name: "myauthor_headphones"` must be in a file named `myauthor_headphones.json`.

##### Example Wearable Definition

`game/mod_assets/sayori/sitting/jsons/myauthor_headphones.json`:
```json
{
    "reference_name": "myauthor_headphones",
    "display_name": "Cool Headphones",
    "unlocked": true,
    "category": "accessory",
    "author": "MyAuthor"
}
```

#### Wearable Assets

These are the images the player will see. They must be 1280x720 `.png` files. The folder structure is very specific.

The general path for assets is: `game/mod_assets/sayori/sitting/[folder]/[reference_name]/[asset_name].png`

The `[folder]` and `[asset_name].png` change based on the category:

- **For `clothes`:**
  - `body/[reference_name]/1.png`
  - `arms/[reference_name]/back-arm.png`
  - `arms/[reference_name]/folded.png`
  - `arms/[reference_name]/left-index-point.png`
  - `arms/[reference_name]/...` (and so on for each arm pose you want to support)

- **For `hairstyle`:**
  - `hair/[reference_name]/a.png`

- **For `eyewear`, `accessory`, `headgear`, `necklace`:**
  - `[category]/[reference_name]/sitting.png` (e.g., `accessory/myauthor_headphones/sitting.png`)

### 2. Creating New Custom Outfits

An outfit is a complete combination of wearables that Sayori can be asked to wear.

#### Outfit Definition File

This is a `.json` file that defines an outfit by combining existing wearables. It must be placed in the `game/mod_assets/sayori/sitting/jsons/` directory.

The file **must** include:

- `reference_name`: A unique internal name for the outfit.
- `display_name`: The name of the outfit shown in-game.
- `unlocked`: Should be `true`.
- `clothes`: The `reference_name` of a `clothes` wearable.
- `hairstyle`: The `reference_name` of a `hairstyle` wearable.

The following are **optional**:

- `eyewear`
- `accessory`
- `headgear`
- `necklace`

##### Example Outfit Definition

`game/mod_assets/sayori/sitting/jsons/myauthor_test_outfit.json`:
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

---

## Advanced Method: Using `.rpy` Files

This method provides full control over your wearables and outfits, allowing for dynamic and conditional logic. It requires creating a `.rpy` file in the `game/` folder (e.g., `game/submods/my_clothes.rpy`).

### 1. Creating Image Files

First, create the image assets for your wearable and place them in the correct folder structure as described in the `.json` method. For a t-shirt named `myauthor_cool_shirt`, the paths would be:
- `game/mod_assets/sayori/sitting/body/myauthor_cool_shirt/1.png`
- `game/mod_assets/sayori/sitting/arms/myauthor_cool_shirt/folded.png`
- ...and so on for all arm poses.

### 2. Registering Wearables and Outfits

Next, you'll write Python code in your `.rpy` file to register your creations. This should be done in an `init` block with a priority of 5 (`init 5 python:`).

The process involves two main steps:
1.  **Register Wearables:** Define each individual piece of clothing (`FAEClothes`, `FAEHairstyle`, etc.).
2.  **Register Outfits:** Combine the registered wearables into a complete `FAEOutfit`.

Here is a complete example for `game/submods/myauthor_cool_outfit.rpy`:

```python
# game/submods/myauthor_cool_outfit.rpy

init 5 python:
    # Import the outfits module to access its classes and functions
    import store.fae_outfits as fae_outfits

    # --- PART A: Register Individual Wearables ---
    # Each piece must be registered as a wearable object before it can be used in an outfit.

    # Example: Register a new T-shirt
    fae_outfits._m1_new_outfits__register_wearable(
        fae_outfits.FAEClothes(
            reference_name="myauthor_cool_shirt", # Unique code name
            display_name="Cool T-Shirt",          # Name shown to the player
            unlocked=True,                        # Unlocked from the start
            is_fae_wearable=False,                # Always False for submod content
            author="MyAuthor"                     # Your author name
        )
    )

    # Example: Register a new hairstyle
    fae_outfits._m1_new_outfits__register_wearable(
        fae_outfits.FAEHairstyle(
            reference_name="myauthor_spiky_hair",
            display_name="Spiky Hair",
            unlocked=True,
            is_fae_wearable=False,
            author="MyAuthor"
        )
    )

    # --- PART B: Register the Complete Outfit ---
    # Now, combine the registered wearables into an outfit.

    fae_outfits._m1_new_outfits__register_outfit(
        fae_outfits.FAEOutfit(
            reference_name="myauthor_rocker_style", # Unique code name for the outfit
            display_name="Rocker Style",          # Name shown to the player
            unlocked=True,                        # Is the outfit unlocked?
            is_fae_outfit=False,                  # Always False for submod content

            # Use get_wearable() to retrieve the pieces registered above
            clothes=fae_outfits.get_wearable("myauthor_cool_shirt"),
            hairstyle=fae_outfits.get_wearable("myauthor_spiky_hair"),

            # For optional pieces, you can use existing ones or your own.
            # To leave a slot empty, omit the parameter or use get_wearable("fae_none").
            accessory=fae_outfits.get_wearable("fae_none"),
            eyewear=fae_outfits.get_wearable("fae_none"),
            headgear=fae_outfits.get_wearable("fae_none"),
            necklace=fae_outfits.get_wearable("fae_none")
        )
    )
```

The `is_fae_wearable` and `is_fae_outfit` flags should always be set to `False` for submod content. This tells the game that the content is from a submod.

### Conditional Unlocking

The main advantage of the `.rpy` method is conditional logic. You can make a wearable unlock only when certain conditions are met by passing a function or `lambda` to the `unlocked` parameter.

**Example:** An "Awesome Outfit" that only unlocks at 500 affection.

```python
init 5 python:
    import store.fae_outfits as fae_outfits
    import store.fae_affection as Affection # Import the affection module

    fae_outfits._m1_new_outfits__register_wearable(
        fae_outfits.FAEClothes(
            reference_name="myauthor_awesome_outfit",
            display_name="Awesome Outfit",
            # This function is checked in real-time
            unlocked=lambda: Affection.getAffection() >= 500,
            is_fae_wearable=False,
            author="MyAuthor"
        )
    )
```

---

## Adding Outfit Reactions

You can make Sayori react to changing into a specific wearable. The system is designed to be easily extended without modifying core files.

When the player applies a clothing change, the game looks for a Ren'Py `label` with a specific name and runs it. The naming convention is: `reaction_<category>_<reference_name>`.

To add a reaction, simply create a label with the correct name in your submod's `.rpy` file.

**Example:** Adding a reaction for the "myauthor_cool_shirt" wearable created earlier.

```renpy
# game/submods/myauthor_cool_outfit.rpy

label reaction_clothes_myauthor_cool_shirt:
    s "Oh, this T-shirt is so cool! I feel like a rock star."
    s "Thanks for picking it out for me, [player]!"
    return
```

The game will automatically find and execute this label when the player puts on the "Cool T-Shirt". If the label doesn't exist, nothing happens.
