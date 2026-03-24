# Backgrounds System

The backgrounds system allows you to change the background of the room.

## How it Works

The `game/additional/bgs.rpy` file manages backgrounds. It uses:

* `Rooms` to define each room/background.
* `FAERooms` to manage current room state, transitions, and day/night switching.

The system automatically switches between day and night images based on local time.

## Adding New Backgrounds

To add a new background, you need to create a submod that does the following:

1.  **Create the background images:** You need to create day and night versions of your background image. The images must be in PNG format and named as follows:
    *   `{id}-day.png`
    *   `{id}-night.png`

    Replace `{id}` with a unique identifier for your background. These images should be placed in a new folder inside `mod_assets/rooms/`. For example: `mod_assets/rooms/my_new_room/`.

2.  **Register the background:** Use `register_room` in an `init` block in your submod `.rpy`.

Here's an example of how to register a background:

```renpy
init 5 python:
    import store.fae_rooms as fr
    fr.register_room(
        "my_new_room",
        "my_new_room",
        display_name=_("My New Room")
    )
```

### `register_room` Parameters

*   `id` (str): A unique ID for the background. This should match the name used in the image files.
*   `image_directory` (str): The name of the directory where the background images are located (inside `mod_assets/rooms/`).
*   `display_name` (str): The translatable name shown in the room selection UI.
*   `decoration_permitted` (list, optional): A list of strings representing categories for decorations that are supported for this background.
*   `when_enter` (callable, optional): A function to run when changing into this background.
*   `when_leave` (callable, optional): A function to run when leaving this background.

`display_name` is required by the underlying `Rooms` constructor, so include it explicitly.
