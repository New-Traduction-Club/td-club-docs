# Backgrounds System

The backgrounds system allows you to change the background of the room.

## How it Works

The `additional/bgs.rpy` file manages the backgrounds. It uses a `Rooms` class to define each background and a `FAERooms` class to manage the current room and handle transitions.

The system automatically switches between day and night versions of the background based on the time of day.

## Adding New Backgrounds

To add a new background, you need to create a submod that does the following:

1.  **Create the background images:** You need to create day and night versions of your background image. The images must be in PNG format and named as follows:
    *   `{id}-day.png`
    *   `{id}-night.png`

    Replace `{id}` with a unique identifier for your background. These images should be placed in a new folder inside `mod_assets/rooms/`. For example: `mod_assets/rooms/my_new_room/`.

2.  **Register the background:** You need to register your background so it appears in the background selection screen. You can do this by calling the `register_room` function in an `init` block in your submod's `.rpy` file.

Here's an example of how to register a background:

```renpy
init 5 python:
    import store.fae_rooms as fr
    fr.register_room("my_new_room", "my_new_room")
```

### `register_room` Parameters

*   `id` (str): A unique ID for the background. This should match the name used in the image files.
*   `image_directory` (str): The name of the directory where the background images are located (inside `mod_assets/rooms/`).
*   `decoration_permitted` (list, optional): A list of strings representing categories for decorations that are supported for this background.
*   `when_enter` (callable, optional): A function to run when changing into this background.
*   `when_leave` (callable, optional): A function to run when leaving this background.

By following these steps, you can easily add new backgrounds to the game!
