> Warning: This guide only applies to the version of the port with the material-themed menu, export persistent, file explorer, etc.
>
> We recommend backing up your progress using the `Export Persistent` option to avoid any issues with the migration script.

1. Download [this rpy file](https://files.traduction-club.live/docs/jnl/a_persistent_migration.rpy). <br>
This is a script to migrate persistent from Ren'Py 8.3.7 to Ren'Py 6.99.

2. Place the rpy script you downloaded at: `InternalFiles/game/`
    <details>
    <summary>More details</summary>
        <b>Open Internal Files Explorer.</b>
        ![img](https://files.traduction-club.live/docs/jnl/img02.webp)
        <br>
        <b>Go to game folder.</b>
        ![img](https://files.traduction-club.live/docs/jnl/img03.webp)
        <br>
        <b>Tap on Import button, select `Import files` option.<br>
        Select your `a_persistent_migration.rpy`, then import it.</b>
        ![img](https://files.traduction-club.live/docs/jnl/img04.webp)
    </details>

3. Open JN and exit.

4. Use `Export persistent` button.

5. Open JNL, use `Import Persistent`, use Zip file from step 4.

6. On Start Menu go to: See more > Save files > `saves` folder. <br>
    Delete `persistent` and any `*.save` file. <br>
    Rename `persistent_699` to `persistent`.
    <details>
    <summary>More details</summary>
        <b>Before.</b>
        ![img](https://files.traduction-club.live/docs/jnl/img08.webp)
        <br>
        <b>After.</b>
        ![img](https://files.traduction-club.live/docs/jnl/img11.webp)
    </details>

7. All ready!
