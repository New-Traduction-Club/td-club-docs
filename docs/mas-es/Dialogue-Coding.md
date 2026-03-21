# Estructura del diálogo

```renpy
init 5 python:
    addEvent(
        Event(
            persistent.event_database,
            eventlabel="monika_twitter",
            category=['monika'],
            prompt="Twitter",
            random=True
        )
    )

label monika_twitter:
    m 1eud "Did you know I'm on Twitter?"
    # ...
    return
```

Al diálogo estándar (el que puede salir de forma aleatoria o el que activas con la opción "Say/Hey Monika") normalmente se le llama `topic`. Crear un `topic` tiene dos partes: el `init 5 block` y el diálogo en sí. Ese `init 5 block` define las propiedades del `topic`, así que ahí decides cómo se mostrará y dónde podrá aparecer.

## El bloque `init 5 python`

Aunque hablemos de "topic" en el día a día, internamente todo esto es un `Event`. El bloque `init 5` se usa para asignar propiedades a esos `Event` y para registrar en el sistema que ese `Event` existe.

El objeto `Event` acepta bastantes propiedades; aquí tienes las más habituales:
```renpy
init 5 python:
    addEvent(
        Event(
            persistent.event_database,
            eventlabel="monika_topic_name",
            category=["category name", "another category name"],
            prompt="Prompt Name",
            random=True,
            pool=True,
            conditional="<python_expression_here>",
            action=<EV_ACTION_HERE>,
            start_date=datetime.date.today(),
            end_date=datetime.date.today() + datetime.timedelta(days=1),
            rules={},
            aff_range=(mas_aff.NORMAL, None)
        )
    )
```

#### Propiedades:

* `eventlabel`:
  - Es la label de tu topic.
  - Debe coincidir con la label del diálogo real.
  - En topics estándar, lo normal es usar el prefijo **`monika_`**.
  - **Esto es obligatorio.**
* `category`:
  - Lista de categorías a las que pertenece el topic.
  - Conviene escribirlas siempre en minúsculas.
  - Se usa al ver el topic en "Repeat Conversation" o "Hey Monika".
  - **Si no la defines, el topic aparecerá en la lista principal de categorías en vez de dentro de una categoría concreta.**
* `prompt`:
  - Texto que aparece en el botón para activar el topic.
  - Si el `prompt` funciona como título, escríbelo con formato de título. Si no, normalmente basta con mayúscula inicial.
  - Se usa en cualquier parte del "Talk Menu".
  - **Si no defines un `prompt`, se mostrará `eventlabel` en su lugar.**
* `random`:
  - `True` permite que este topic aparezca aleatoriamente.
  - Suele usarse en topics donde Monika inicia la conversación. (**Predeterminado:** `False`)
* `pool`:
  - `True` permite que este topic aparezca en Unseen y también en "Hey Monika".
  - Suele usarse en topics que inicia el jugador. (**Predeterminado:** `False`)
* `conditional`:
  - Es una condición, en formato string, que debe cumplirse para ejecutar la propiedad `action` del topic.
  - Por sí sola aporta poco si no hay ninguna `action` definida.
* `action`:
  - Acción automática que se ejecuta cuando se cumplen `conditional` y, si aplica, `start_date` y `end_date`.
  - Acciones disponibles:
    - `EV_ACT_QUEUE`:
      - Encola el evento
    - `EV_ACT_PUSH`:
      - Hace push del evento
    - `EV_ACT_RANDOM`:
      - Convierte el evento en aleatorio
    - `EV_ACT_POOL`:
      - Convierte el evento en pool
    - `EV_ACT_UNLOCK`:
      - Desbloquea el evento
* `start_date`:
  - Marca la `date`/`datetime` a partir de la cual se puede mostrar el evento.
  - Esta fecha es inclusiva. (la `action` puede ejecutarse en esa fecha)
* `end_date`:
  - Marca la `date`/`datetime` a partir de la cual el evento deja de estar disponible.
  - Como `datetime.date`, es exclusiva, lo que significa que el último día en que la `action` puede ejecutarse es el día anterior al `end_date`.
  - Como `datetime`, mientras la hora actual sea anterior a la hora de `end_date`, la `action` puede ejecutarse.
* `years`:
  - Define en qué años se mantendrán `start_date`, `end_date` y `conditional` para ese topic (la `action` podrá volver a activarse en esos años si se cumple todo, y esas propiedades **no** se borrarán tras ejecutarse).
  - Si pasas una lista vacía (`[]`), el topic se repetirá cada año.
* `rules`:
  - Un diccionario de reglas para el evento.
  - Reglas disponibles:
    - `"no_unlock"`:
      - Solo se aplica a topics `pool`.
      - No acepta valor.
      - Garantiza que el topic no se desbloquee mediante desbloqueos aleatorios del pool.
    - `"skip alert"`:
      - Solo se aplica a topics `random`.
      - No acepta valor.
      - Garantiza que, cuando Monika saque este topic, no aparezca ninguna alerta.
    - `"bookmark_rule"`:
      - Valores aceptados:
        - `mas_bookmarks_derand.WHITELIST` - Marca este topic como apto para marcadores. (úsalo si el `eventlabel` no tiene un prefijo aceptable)
        - `mas_bookmarks_derand.BLACKLIST` - Marca este topic como no apto para marcadores. (úsalo si el topic no debería poder marcarse aunque tenga un prefijo aceptable)
    - `"notif-group"`:
      - Acepta un valor de notif-group. (string que indica el grupo bajo el que se enviará la notificación)
      - Solo se aplica a WindowReacts.
    - `"force repeat"`:
      - Solo se aplica a topics aleatorios.
      - No acepta valor.
      - Obliga a que este topic sea repetible incluso si repeat topics está en `False`.
      - En general, NO deberías usarlo en topics. Las excepciones suelen ser topics ligados a eventos o topics aleatorios delegados.
    - `"no_rmallEVL"`:
      - Solo se aplica a topics con una `MASUndoActionRule` registrada que quitará el modo aleatorio al topic.
      - No acepta valor.
      - Garantiza que el topic no se quite de la lista de eventos cuando se ejecute la Undo Action Rule y se le quite el modo aleatorio.
* `unlocked`:
  - `True` hará que este topic aparezca por defecto en su colección correspondiente (Hey Monika/Repeat Conversation).
  - En la práctica, normalmente solo necesitarás usarlo en `True` para topics `pool`. (**Predeterminado:** `False`)
* `aff_range`:
  - Limita la disponibilidad del topic según el afecto actual de Monika.
  - `None` indica rango sin límite, así que `(mas_aff.NORMAL, None)` significa disponible desde afecto NORMAL en adelante.

##### Cosas a tener en cuenta:
**Las siguientes propiedades NO se cambiarán si ya existen objetos de evento para ese `eventlabel` (al cargar con `addEvent` para ese `eventlabel`):**

- `random`
- `unlocked`
- `pool`
- `conditional`
- `action`
- `start_date`
- `end_date`

`aff_range`, `category`, `rules` y `prompt` sí se actualizarán siempre al valor definido en `addEvent`.

#### Niveles de afecto disponibles:

* `BROKEN` - Monika parece rota
* `DISTRESSED` - Monika se ve triste
* `UPSET` - Monika muestra una expresión neutra y desinteresada. **Aquí upset no se usa en su sentido literal**
* `NORMAL` - Afecto estándar. Monika tiene la sonrisa estándar (1eua)
* `HAPPY` - Monika muestra expresiones más alegres
* `AFFECTIONATE` - Monika está cariñosa
* `ENAMORED` - Monika está enamorada del jugador
* `LOVE` - Monika está completamente cómoda con el jugador

Si quieres profundizar, consulta `definitions.rpy` para ver la lista completa de propiedades. Muchas son específicas de ciertos tipos de eventos y **no están pensadas para diálogo estándar**.

## Diálogo

El diálogo usa la sintaxis estándar de Ren'Py. El formato general es:

```renpy
m spritecode "Dialogue"
```

## Claves de retorno
Si revisas algunos diálogos, verás que ciertos topics terminan con `return "derandom"`, `return "no_unlock"`, `return "love"` y, en algunos casos, con una combinación como `return "love|derandom"`.

Cada clave de retorno tiene un efecto distinto. Aquí tienes las disponibles y para qué sirve cada una:

- `"derandom"`:
  - Solo tiene efecto en topics aleatorios.
  - Quita el modo aleatorio del topic después de terminar.

- `"no_unlock"`:
  - Funciona SOLO para topics aleatorios.
  - Garantiza que el topic no se desbloquee (es decir, que no muestre su `prompt`) en repeat conversation.
  - NOTA: Esto no tiene efecto si el topic ya está desbloqueado cuando se devuelve esta clave.

- `"rebuild_ev"`:
  - Reconstruye las listas de eventos.
  - En la mayoría de casos no lo usarás. Se usa cuando se activa una flag importante que exige regenerar el pool de topics disponibles (por ejemplo, sensitive mode).

- `"idle"`:
  - Pone MAS en modo idle (modo brb, «vuelvo enseguida»).
  - Se usa al final de eventos brb para entrar en modo idle.

- `"love"`:
  - Cambia el prompt "I love you!" de la pantalla principal de conversación por "I love you too!".
  - Debería usarse si el topic incluye "I love you" cerca del final.

- `"quit"`:
  - Permite que Monika cierre el juego por sí misma (de forma segura).
  - Debería usarse para despedidas.

- `"prompt"`:
  - Te devuelve a la pantalla principal de conversación desde el topic.
  - Debería usarse en topics que empiezan con un `mas_gen_scrollable_menu` o algo parecido como parte de la opción `Nevermind.`.

## Combinar claves de retorno:
Como en el ejemplo de arriba, puedes combinar claves de retorno poniendo una barra (`|`) entre ellas, ***sin espacios***.

#### El sistema de sprites:
MAS tiene un sistema de sprites muy potente que permite manejar muchas expresiones, poses y más detalles.

El diálogo usa spritecodes (códigos cortos que representan expresiones y poses). Para construirlos de forma visual, puedes usar el [Expression Previewer](./FAQ.md#how-do-i-find-the-spritecode-for-an-expression).

Cuando lo uses un poco, verás que los spritecodes aparecen en texto rosa o rojo.
- Si un spritecode aparece en **rosa**, el sprite existe en el código fuente actual y puede usarse sin problemas en tus diálogos.
- Si un spritecode aparece en **rojo**, el sprite *no* existe en el código fuente actual y usarlo en diálogo hará que Monika desaparezca.

Aun así, que eso no te frene. Si crees que ese sprite encaja con tu diálogo, añádelo. También hay un conjunto de herramientas pensado para ayudarte a crear estos sprites, y lo vemos justo en la siguiente sección.

#### El menú de herramientas:
En el código fuente de Monika After Story hay un archivo concreto con utilidades muy prácticas.

Ve a `MonikaModDev/tools/toolsmenu.py` y ejecútalo con Python 2. Verás algo así:

```
#=============================================================================#
#   MAS Dev Tools                                                             #
#=============================================================================#

    1) Sprite Puller
    2) Check Sprites
    3) Make Sprites
    4) Generate Expressions Test

   [0] Exit


Utility:
```

##### Las utilidades:
1) **Sprite Puller**
```
#=============================================================================#
#   Sprite Puller                                                             #
#=============================================================================#

    1) Generate Sprite Code List
    2) Generate Optimized RPY

   [0] Exit


Option:
```

- En general, no sueles necesitar esta utilidad.
- Lo más útil aquí suele ser la primera opción, que genera una lista de sprites para Monika (se exporta a `MonikaModDev/tools/zzzz_spritelist`).

2) **Check Sprites**
```
#=============================================================================#
#   Include Dev?                                                              #
#=============================================================================#

    1) Yes
    2) No

   [0] Exit


Option:
```

- Esta opción recorrerá los archivos rpy de la carpeta `/game` del repositorio y comprobará si todos los spritecodes usados (`m spritecode "dialogue"`, `extend spritecode "dialogue"`, `show monika spritecode`, etc.) son válidos.
- Si detecta errores, la herramienta lo indicará y exportará una lista de spritecodes no válidos con sus archivos y números de línea en `MonikaModDev/tools/zzzz_badcodes.txt`.
- Para esto, no deberías necesitar `Include Dev`.

3) **Make Sprites**
```
#=============================================================================#
#   Sprite Maker                                                              #
#=============================================================================#

    1) List Codes
    2) Make Sprite (Interactive)
    3) Make Sprite (By Code)
    4) Generate Sprites

   [0] Exit


Option: 
```

- Esta opción te permite generar tus sprites.
- La primera subopción te deja ver una lista de todos los spritecodes con filtros por rasgos concretos (pose, ojos, boca, etc.).
- La siguiente opción te permite crear sprites guiándote parte por parte de la expresión y, para las partes opcionales, decidir si incluirlas o no.
  - Por ejemplo: qué tipo de ojos quieres (normal, winkleft, smug, etc.) o si quieres rubor (y de qué tipo).
- La tercera opción te permite crear sprites por spritecode. Si ya conoces el sistema de expresiones o has usado el expression previewer para montar el sprite que quieres, introduce su código y esta opción lo construirá por ti.
- La opción final se usa para exportar los sprites que has creado a los archivos de sprite-chart. Úsala al terminar y asegúrate de confirmar la sobrescritura de los archivos rpy para guardar los cambios.

4) **Generate Expressions Test**
- Esto te será prácticamente inútil, porque no hará nada en tus scripts.


## Crear diálogo con menús

MAS usa su propia forma de menús; la estructura a seguir es esta:
```renpy
m expression "Question?{nw}"
$ _history_list.pop()
menu:
    m "Question?{fast}"

    "Option 1":
        #Dialogue/code for this path

    "Option 2":
        #Dialogue/code for this path

    #...:
        #...
```

#### Cosas a tener en cuenta:

- La etiqueta `{nw}` en la primera línea de pregunta: así el jugador ve la pregunta antes de que aparezcan las opciones, y estas salen automáticamente.
- El `$ _history_list.pop()` tras la primera línea de pregunta: así la pregunta solo aparece una vez en la pestaña de historial.
- La ausencia de `expression` en la segunda línea de pregunta: los menús no aceptan expresiones dentro de ellos.
- La etiqueta `{fast}` en la segunda línea de pregunta: así la línea se muestra al instante cuando aparecen las opciones del menú.

## Uso de `if`, `elif` y `else`:

`if` se usa cuando quieres ejecutar código o mostrar diálogo si una condición es `True`.

`elif` se usa *después* de un `if`. También tiene su condición, y se evalúa si la de arriba fue `False`.

`else` es el caso de *respaldo*. Si ninguna condición de `if` o `elif` se evalúa como `True`, se ejecuta `else`. (Aunque no es obligatorio encadenarlo con `if` o `elif`)

#### Ejemplo:
```python
x = 3
if x == 1:
    print("x is 1!")

elif x == 3:
    print("x is 3!")

#There can be more conditions between here

else:
    print("x isn't 1 or 3!")
```

En este ejemplo se ejecuta el bloque `elif`, y se imprimiría `"x is 3!"`.

NOTA: las comparaciones de igualdad se hacen con `==`, no con `=`.

Si estás comparando variables de tipo `string`, usa esta forma:

```python
if stringvar.lower() == "comparison":
    pass
```

- Esto se hace porque `"Hello"` __no__ es lo mismo que `"hello"`.

## Tener respuestas diferentes al revisitar un topic
Puedes consultar cuántas veces se ha visto un topic con `mas_getEV("eventlabel").shown_count`. (NOTA: `eventlabel` debe ser válido o recibirás un error)

Si quieres que el diálogo cambie al repetir topics, puedes comprobar `shown_count` *durante* el topic, ya que solo se actualiza después de verse.

#### Ejemplo:
```renpy
label monika_example:
    $ ev = mas_getEV("monika_example")

    if ev.shown_count == 0:
        m 1hub "This is the first time you've seen this topic!"

    elif ev.shown_count == 1:
        m 3eub "This is the second time you've seen this topic."

    #You can keep going here

    else:
        m 1wud "Wow [player], you've seen this topic so many times!"
    return
```

## Uso de condicionales
La propiedad `conditional` de un `Event` permite que la propiedad `action` de tu topic se ejecute cuando el `conditional` se evalúa como `True`.

#### Condicionales basados en tiempo:
Si quieres que tu topic se active en un momento concreto mientras el jugador está con Monika, los `Event` incluyen dos propiedades para eso: `start_date` y `end_date`.

Estas pueden ser objetos `datetime.datetime` o `datetime.date` y funcionarán junto con `conditional` si está presente (también puedes usar solo fechas start/end o solo `conditional`).

Estas propiedades también pueden disparar la propiedad `action`.

#### Las acciones posibles son:

- `EV_ACT_QUEUE` - *encola* un evento
- `EV_ACT_PUSH` - hace *push* de un evento (prioridad más alta que queue)
- `EV_ACT_RANDOM` - pone la propiedad `random` del evento en `True` (puede aparecer en charla aleatoria)
- `EV_ACT_POOL` - pone la propiedad `pool` del evento en `True` (puede accederse mediante la opción `Hey [m_name]...` en la pantalla `Talk`)
- `EV_ACT_UNLOCK` - desbloquea el evento (NOTA: esto solo permite que el evento se vea en las secciones `repeat conversation` o `Hey [m_name]...` de la pantalla `Talk`)

#### Cosas a tener en cuenta:

- El `conditional` ***debe*** escribirse como un `string`.
- La condición también ***debe*** poder evaluarse en `init 5` (no puedes usar métodos definidos en niveles de init más altos).
- Usar una fecha de inicio o fin hará que el `prompt` del evento (`eventlabel` si no está presente) aparezca en el calendario por defecto. (Puedes evitarlo con el parámetro `skipCalendar`)
- Los `end_date` ***no*** son inclusivos. Los `start_date` sí lo son.

#### Ejemplo:
```renpy
init 5 python:
    addEvent(
        Event(
            persistent.event_database,
            eventlabel="monika_example",
            prompt="The Southern hemisphere"
            category=["misc"],
            conditional="persistent._mas_pm_lives_south_hemisphere",
            start_date=datetime.date(2019, 4, 15),
            end_date=datetime.date(2019, 4, 16)
            action=EV_ACT_PUSH
        )
    )

label monika_example:
    #dialogue
    return
```

Este topic de ejemplo hará push si le dices a Monika que vives en el hemisferio sur y es entre el 15 y el 16 de abril de 2019.
