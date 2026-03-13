# WORKING WITH THE SUBMOD MATRIX

<!-- When v0.1: New Beginnings released, it contained the inclusion of a submod system. -->
Submods are ways for players to add their own content to the mod, without dev review/approval.

Players of MAS will find this system easy to understand, since I've made it as similar as possible for ease of use.

# USING THE SUBMOD SYSTEM

The `submod` system is basically a way to let the game know you're adding extra content.

It **must** be done in an `init -991 python in fae_extras` block.

If run at another runlevel, dependancies will not be checked.

An example of the beginning of a submod would be the following

```renpy
init -991 python in fae_extras:
    Extras(
        creator="Forever And Ever Team",
        name="Submod example",
        description="An example submod."
    )
```


The above code will import a submod with this information:

- Creator: `Forever And Ever Team`
- Name: `Submod example`
- Description: `An example submod.`

When creating dialogue submods, please try and adhere to the [Coding Style](https://github.com/Just3090/justsayori-mod/wiki/Coding-Style)

## Submodding Guides

Here are some guides to help you create your own submods:

*   **[Gifting System](./Gifting-System.md)**: Learn how to add new gifts for Sayori.
*   **[Minigame Hub](./Minigame-Hub.md)**: Learn how to add new minigames to the hub.
*   **[Backgrounds System](./Backgrounds-System.md)**: Learn how to add new backgrounds to the game.
*   **[Outfits & Wearables](./Outfits.md)**: Learn how to add new outfits and clothing for Sayori.
