# Virtual Desktop

![img](https://files.traduction-club.live/docs/masl/img01.webp)
Dark mode variant:
![img](https://files.traduction-club.live/docs/masl/img02.webp)

## Main Options

### Start game

As the name suggests, it will run _Monika After Story_. If you haven't installed MAS or deleted its folder (`monikaafterstory-masl-edition`), it will try to start, but it won't have anything to run and will do nothing.

### Browse Internal Files

It opens the File Explorer at [`filesDir()`](https://developer.android.com/reference/android/content/Context#getFilesDir()), where you can browse and open files with the built-in file viewer. You can also delete, copy, cut, search, rename, and create folders and files.

### Import persistent

You will be able to select and import a zip file on `SaveFiles/saves/`. Follow the instructions in the pop-up dialog.

### Export persistent

You will be able to export the contents of the `SaveFiles/saves/` folder as a zip file.

### Settings

You can change language (English, Spanish, Portuguese) of Virtual Desktop, button sound effect and the window mode.

### See more

It expands Start Menu to show Save Files, Update game, Backups, Wallpapers, App Info and Experiments.

#### Save Files

It opens the File Explorer at [`ExternalFilesDir()`](https://developer.android.com/reference/android/content/Context#getExternalFilesDir(java.lang.String)).

#### Update game

You will be able to install/update our Monika After Story version for MASL 6.99, reading this [list](https://raw.githubusercontent.com/New-Traduction-Club/MASL-6.99/refs/heads/main/.utilityfiles/packages_list.json).

#### Backups

Screen to backup/restore all content of `filesDir()`/Internal Files based on Zip files stored at `SaveFiles/backups`.

#### App Info

It shows the app version, logo, commit of the build, and other kinds of information.

#### Experiments

See [this section](./Experiments.md).
