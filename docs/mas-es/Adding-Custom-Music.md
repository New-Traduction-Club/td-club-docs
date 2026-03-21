La versión 0.8.1 añadió soporte para música personalizada (OGG/VORBIS) en MAS ([#1592](https://github.com/Monika-After-Story/MonikaModDev/pull/1592)).

La versión 0.8.2 añadió soporte para formatos de música adicionales (MP3, OPUS), además de bucles mediante etiquetas de metadatos (datos del archivo como artista y título) ([#1670](https://github.com/Monika-After-Story/MonikaModDev/pull/1670), [#1695](https://github.com/Monika-After-Story/MonikaModDev/pull/1695)).

La versión 0.12.18 _modified by TD Club_ tiene como formatos soportados: MP3, OGG, VORBIS, OPUS, WAV, FLAC.

# Añadir música personalizada
Para añadir música personalizada, sigue estos pasos:

> Nota: La carpeta `DDLC/` en Android (MASL) corresponde a `Archivos Internos`.

1. Asegúrate de que la música que quieres añadir esté en formato MP3, OGG/VORBIS, OPUS o los formatos extra si estas usando la versión modificada por TD Club.
2. Crea la carpeta `custom_bgm/` en tu directorio `DDLC/` si todavía no existe.

> En MASL debes crear la carpeta `custom_bgm/` dentro de `game/`.

3. Coloca los archivos de música en esa carpeta.
4. Inicia el juego.

## Nombres de canciones
En la versión 0.8.1, los archivos se muestran en el menú de música con su nombre de archivo.

En la versión 0.8.2+, los archivos se muestran en el menú de música con sus etiquetas de metadatos, así:
```
Artist - Title
```
Si no existe la etiqueta Artist, se usa solo la etiqueta Title. Si no existe la etiqueta Title, se usa el nombre del archivo.

# Bucle
**Esto solo está disponible en 0.8.2+**

Por defecto, las canciones se repiten de forma normal (de principio a fin). Para cambiar los puntos de bucle (los segundos concretos en los que la canción vuelve a empezar), ofrecemos 2 formas:

1. Usar etiquetas de bucle de MAS
2. Usar etiquetas de bucle con estilo RPGMaker

NOTA: Los puntos de bucle indican dónde el audio va a **repetirse**, **no dónde va a empezar**.

Es decir, las canciones siempre empezarán desde el principio, pero al llegar al final de la canción o a un punto de fin de bucle, empezarán en el punto de inicio de bucle (si se ha definido).

## Etiquetas de bucle de MAS
**Las etiquetas de bucle de MAS solo funcionan con archivos OGG/VORBIS y OPUS**

1. Abre el archivo de audio en audacity (o en un programa similar).
2. Expórtalo como OGG/VORBIS u OPUS y edita sus metadatos.
3. Añade etiquetas de metadatos:
   1. Añade una etiqueta `masloopstart` y especifica la marca de tiempo (en segundos) donde debe empezar el bucle. 

      _Si no se indica, el inicio de la canción se considera el punto de inicio del bucle._

   2. Añade una etiqueta `masloopend` y especifica la marca de tiempo (en segundos) donde debe terminar el bucle. 
      
      _Si no se indica, el final de la canción se considera el punto de fin del bucle._
4. Guarda los cambios y coloca el archivo de audio en la carpeta `custom_bgm/`.

## Etiquetas de bucle de RPGMaker
**Las etiquetas de bucle de RPGMaker solo funcionan con archivos OGG/VORBIS**

Sigue las instrucciones de [este enlace](https://rpgmaker.net/tutorials/1341/)
