# Compatibility with Submods

The compatibility for submods will be the same as official MAS version or the MAS version that we have edited, both running on MASL 6.99.

> Note that to have the same compatibility on the official MAS, you need to copy `cacert.pem` from `InternalFiles/monikaafterstory-masl-edition/game/python-packages/certifi/` to `YourMASInstallation/../certifi/`. This solves an SSL bug that appears on Android. This is the only action required, as an sslwarp error was resolved internally in the bundled Ren'Py runtime of the app.