La versión 0.8.4 añadió soporte para canciones de piano personalizadas en el minijuego de piano.

# Índice
1. [Formato JSON](./Adding-Custom-Piano-Songs.md#the-format)
   1. [Descripción del formato JSON](./Adding-Custom-Piano-Songs.md#object-explanation)
   2. [Mapa nota-tecla del piano](./Adding-Custom-Piano-Songs.md#notes)
2. [Ubicación del JSON](./Adding-Custom-Piano-Songs.md#location)
3. [Comprobar que los JSON son correctos](./Adding-Custom-Piano-Songs.md#checking-for-correctness)
4. [Problemas conocidos](./Adding-Custom-Piano-Songs.md#known-issues)
5. [Enviar canciones de piano](./Adding-Custom-Piano-Songs.md#submitting-piano-songs)

<a id="the-format"></a>
# El formato

Todas las canciones de piano se guardan en archivos de texto con formato [JSON](https://www.json.org) (un formato para guardar datos estructurados).
Aquí tienes un ejemplo de cómo se anota una canción de piano (muy corta) en JSON:
```json
{
    "name": "Song name",
    "verse_list": [0, 5, 10, 23],
    "pnm_list": [
        {
            "text": "This is a song lyric",
            "style": "monika_credits_text",
            "notes": [
                "D5",
                "C5SH",
                "B4",
                "F4SH",
                "B4",
                "C5SH",
                "D5",
                "E5",
                "D5",
                "C5SH",
                "B4",
                "A4",
                "G4",
                "D5",
                "E5"
            ],
            "express": "1eub",
            "postexpress": "1eua",
            "vis_timeout": 2.0,
            "verse": 0,
            "posttext": true
        },
        {
            "text": "This is the another song lyric",
            "style": "monika_credits_text",
            "notes": [
                "D5",
                "A4",
                "D5",
                "A4",
                "D5",
                "A4",
                "D5",
                "E5",
                "C5SH"
            ],
            "postnotes": [
                "D5",
                "C5SH"
            ],
            "express": "1eub",
            "postexpress": "1eua",
            "ev_timeout": 1.0
        }
    ]
}
```

<a id="object-explanation"></a>
## Explicación de objetos:
### Pares nombre/valor principales:
* `name`: (`string`) nombre de la canción
    - **debe ser único**
    - También es lo que verá el jugador en el menú de canciones de piano
* `verse_list`: (`list`) lista de índices (`int`) donde empieza cada verso
    - los versos funcionan como checkpoints (puntos de control para no reiniciar toda la canción). Por eso no tienes que empezar Your Reality desde el principio cuando te equivocas.
    - el índice debe ser la posición de la frase de notas en `pnm_list` que representa el inicio de un verso
    - esto usa indexado desde 0
* `pnm_list`: (`list`) lista de frases de notas (`object`)
    - cada frase de notas es un objeto; sus pares nombre/valor se describen abajo
* `_comment`: campo ignorado, útil para añadir comentarios

`name`, `verse_list` y `pnm_list` son **obligatorios**.
Hay parámetros adicionales pensados solo para uso interno o que aún no están listos para publicarse. Para más información, consulta la parte superior de `zz_pianokeys`

### Pares nombre/valor de frases de notas:
* `text`: (`string`) texto que Monika dirá durante este conjunto de notas
* `style`: (`string`) estilo que se aplica al texto
    - `monika_credits_text` es el que usan las canciones incluidas por defecto. Puedes usar otros estilos, pero este suele ser el mejor.
* `notes`: (`list`) lista de notas de esta frase
    - mira abajo para más información sobre las notas
* `postnotes`: (`list`) lista opcional de notas que se pueden tocar después de `notes`
    - se usan para asegurar transiciones suaves entre una frase de notas y otra
    - mira abajo para más información sobre las notas
* `express`: (`string`) código de sprite que se mostrará durante esta frase de notas
    - esto solo se muestra **mientras se están tocando las notas**
* `postexpress`: (`string`) código de sprite que se mostrará cuando la frase de notas se toque correctamente
    - esto se muestra **después de tocar las notas**
    - también se muestra mientras se tocan las postnotes
* `ev_timeout`: (`float`) número de segundos de espera antes de agotar el tiempo de entrada / asumir una nota fallada / reiniciar el verso
    - se usa sobre todo para configurar una ventana de tiempo de entrada más amplia antes de esta frase de notas
    - si no se indica, se usa el timeout por defecto: 1.0 (sin canción) o 3.0 (durante la canción)
* `vis_timeout`: (`float`) número de segundos de espera antes de reiniciar la expresión de Monika / quitar la letra visual
    - se usa sobre todo para mantener durante más tiempo la expresión de Monika o la letra visual antes del reinicio visual
    - esto **no** se extiende a la siguiente frase de notas si el jugador empieza a introducir la siguiente frase
    - si no se indica, se usa el timeout por defecto: 2.5 (sin canción) o 4.0 (durante la canción)
* `verse`: (`int`) índice de verso al que pertenece esta frase de notas
    - esto **debe** coincidir con un número de `verse_list`
* `posttext`: (`bool`) `true` significa que la letra visual seguirá visible después de completar la frase de notas
    - el comportamiento por defecto (`false`) es ocultar la letra justo después de completar la frase de notas.
    - esto **respeta** el ajuste `vis_timeout`
* `_comment`: campo ignorado, útil para añadir comentarios

`text`, `style` y `notes` son **obligatorios**.
Hay parámetros adicionales pensados solo para uso interno o que aún no están listos para publicarse. Para más información, consulta la parte superior de `zz_pianokeys`

<a id="notes"></a>
### Notas
Las notas son simplemente cadenas de texto. Estas son las notas disponibles: (corresponden a notas reales de piano)

| Notas | Tecla predeterminada |
| --- | --- |
| F4 | q |
| F4SH | 2 |
| G4 | w |
| G4SH | 3 |
| A4 | e |
| A4SH | 4 |
| B4 | r |
| C5 | t |
| C5SH | 6 |
| D5 | y |
| D5SH | 7 |
| E5 | u |
| F5 | i |
| F5SH | 9 |
| G5 | o |
| G5SH | 0 |
| A5 | p |
| A5SH | - |
| B5 | [ |
| C6 | ] |

<a id="location"></a>
# Ubicación
Las canciones de piano personalizadas deben guardarse en `piano_songs/` con un nombre de archivo `songname.json`

<a id="checking-for-correctness"></a>
# Comprobar que son correctos
Las advertencias y errores de los JSON de piano se registran en el archivo `pnm.log`. El registro es bastante descriptivo y debería bastar para resolver problemas. **No** se garantiza que el log se escriba durante la partida. La mejor forma de comprobar tus archivos es iniciar el juego y salir.

**MAS (y el minijuego de piano) seguirá funcionando incluso si tu JSON de piano no es válido.**
Las canciones que no se carguen correctamente se ignoran.

<a id="known-issues"></a>
# Problemas conocidos
Los datos de victorias / superadas / falladas de las canciones se guardan internamente y se organizan por nombre de canción. Una vez hayas superado una canción con un nombre concreto, esa canción siempre aparecerá en “tocar una canción”, incluso aunque **el JSON base no sea el mismo.** No tenemos previsto corregir esto, porque probablemente requeriría reescribir cómo almacenamos esos datos.

<a id="submitting-piano-songs"></a>
# Enviar canciones de piano
¿Has hecho una canción para que Monika la cante usando el piano?

Sigue estas instrucciones para enviarla. Ten en cuenta que lo más probable es que **no** añadamos más canciones oficialmente, pero sí recopilaremos JSON y los publicaremos en un paquete de notas de piano (similar a los spritepacks).

Para enviar una canción de piano:

1. Crea una issue
2. Adjunta el JSON a la issue. Si el archivo es demasiado grande, enlázalo en la issue.
3. Incluye el texto `#3765` en la issue.

También puedes enviar solo las notas, aunque eso retrasará su inclusión en los paquetes de notas de piano.
