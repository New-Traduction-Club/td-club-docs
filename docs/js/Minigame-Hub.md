# Minigame Hub

The Minigame Hub provides a centralized and extendable way to add and play minigames.

## How it Works

The `core/mg_core.rpy` file is the heart of the minigame hub. It uses a `MiniGame` class to represent each minigame and a registration system to make them available in the hub.

When the player opens the minigame hub, it displays a list of all registered and unlocked minigames. The player can then select a minigame to play.

## Adding New Minigames

To add a new minigame, you need to create a submod that does the following:

1.  **Create the minigame logic:** This is the Ren'Py code for your minigame, including labels, screens, and any other necessary logic.

2.  **Register the minigame:** You need to register your minigame with the hub so it appears in the list of available games. You can do this by calling the `register_minigame` function in an `init` block in your submod's `.rpy` file.

Here's an example of how to register a minigame:

```renpy
init python:
    from store import register_minigame

    register_minigame(
        label="my_awesome_minigame",
        name="My Awesome Minigame",
        image="mod_assets/images/minigames/my_awesome_minigame_cover.png",
        unlocked=True,
        condition="persistent.my_awesome_minigame_unlocked"
    )
```

### `register_minigame` Parameters

*   `label` (str): The Ren'Py label to call to start the minigame.
*   `name` (str): The display name of the minigame in the hub.
*   `image` (str): The path to the cover image for the minigame.
*   `unlocked` (bool or callable): Determines if the minigame is unlocked. Can be a boolean or a function that returns a boolean.
*   `condition` (str or callable, optional): An additional condition to gate the minigame. Can be a Python expression as a string or a function that returns a boolean.
*   `description` (str, optional): A short description of the minigame.
*   `prep` (callable, optional): A function to be executed before launching the minigame.
*   `pid` (str, optional): A unique persistent ID for the minigame. If not provided, the label is used as the ID.

Happy Bun!