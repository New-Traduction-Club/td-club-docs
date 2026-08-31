# MAICA Compatibility

MASL 6.99 was made to offer the most compatible mobile port with submods rather than Play Store version, MAICA is not the excpetion here.
But you need to make something to run it properly.

After (or before) installing the submod, you need to open this file:
`game/Submods/MAICA_ChatSubmod/api.rpy`
> You can use any text editor, we recommend to use [QuickEdit](https://play.google.com/store/apps/details?id=com.rhmsoft.edit).

At the top of file, search this lines:

```python
init -1500 python:
    if not config.language:
        config.language = "english"
    maica_ver = '1.8.20'
    maica_is_dev = False
    # 如果是开发版本:
    # - workflow不会自动发布release
    # - 对应migration总是会执行
    # - 会显示一条警告
```

You need to add this line: `renpy.android = False`

Here the full example with the edit:

```python
init -1500 python:
    renpy.android = False
    if not config.language:
        config.language = "english"
    maica_ver = '1.8.20'
    maica_is_dev = False
    # 如果是开发版本:
    # - workflow不会自动发布release
    # - 对应migration总是会执行
    # - 会显示一条警告
```
<details>
<summary>Read more</summary>
This change is necesasary to solve the bug where MAICA can't connect to internet on MASL 6.99.
<br>
The port includes a SSL certificate and special tweaks on our Ren'Py build, but the code of the submod have some special conditions for Android, which we're thinking that was made for the chinese mobile port, if we're not mistaken. Since MASL works in a similar way of a normal PC, we can just put False the condition and it will works fine.
</details>

If you update the submod, you may need to do this again.

> Latest version tested: [1.8.20](https://github.com/Mon1-innovation/MAICA_ChatSubmod/releases/tag/1.8.20)