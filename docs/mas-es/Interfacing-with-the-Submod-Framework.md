# El marco de submods está actualmente en plena renovación debido a la migración de MAS a Python 3. Esta página se actualizará a medida que haya novedades.
# Los submods de estilo antiguo pasarán a ser incompatibles; por ahora, evita crear submods nuevos.
# Proporcionaremos una herramienta para convertir submods de estilo antiguo a submods de estilo nuevo.

El marco de submods te permite registrar submods (mini modificaciones personalizadas para MAS) con dependencias y tener scripts de actualización para distintas versiones, lo que ayuda a mantener tus submods compatibles con la versión actual de MAS.

Además, el marco de submods proporciona varias utilidades para ti como desarrollador:

- utilidad para conectar funciones a etiquetas u otras funciones
- utilidad para importar paquetes de Python desde una ruta
- utilidad para cargar módulos de renpy dinámicamente

Esta página contiene instrucciones sobre cómo usar el marco.

# Definir un submod
## Estructura de archivos
- Tienes que definir explícitamente tu submod para que MAS pueda detectarlo y cargarlo correctamente.
- Todos los submods deben colocarse dentro del directorio `game/Submods/`. Se permiten subcarpetas. Ejemplos válidos:
- - `game/Submods/My Submod - more outfits/`
- - `game/Submods/My Submod Pack/My Submod - more dialogues/`
- - `game/Submods/My Submod Pack/My Submod - more backgrounds/`
- Todos los submods deben incluir un archivo de cabecera con la definición del submod.
- Todos los submods deben tener su script de renpy en `rpym` y/o `rpymc`. **Recuerda: `rpy`/`rpyc` no son compatibles y el marco de submods los ignorará**
- - Los submods pueden incluir recursos con otros tipos de archivo: `png`, `jpeg`, `py`, `txt`, etc.; cualquier cosa que necesites

## Archivo de cabecera
En el directorio raíz de tu submod, debes colocar un archivo de cabecera: `header.json`; ¡el nombre y la extensión importan!
Usamos el formato JSON para la cabecera del submod. Puedes encontrar más información sobre ello en internet, así como validadores de JSON. Aquí solo cubriremos la información específica de MAS.

El archivo de cabecera más básico:
```json
{
    "header_version": 1,
    "author": "Monika After Story",
    "name": "Example Submod",
    "version": "0.0.3",
    "modules": [
        "main"
    ]
}
```

Un archivo de cabecera más avanzado:
```json
{
    "header_version": 1,
    "author": "Monika After Story",
    "name": "Example Submod",
    "version": "0.0.3",
    "modules": [
        "main"
    ],
    "description": "This is an example.",
    "dependencies": {
        "Some Other Submod": ["0.0.8", "0.1.5"]
    },
    "settings_pane": "example_submod_screen",
    "version_updates": {
        "monika_after_story_example_submod_v0_0_1": "monika_after_story_example_submod_v0_0_2"
    },
    "coauthors": ["Example Submod co-author"],
    "priority": 0
}
```

Ahora explicaremos todos los campos. La cabecera anterior inicializará un submod con la siguiente información:

- Versión de cabecera: `1`
- - **¡Este campo es obligatorio!**
- - Esta es la versión del esquema de submods de MAS; si en el futuro cambiamos drásticamente el marco (algo poco probable), también cambiaremos este número para evitar cargar submods que aún no admitan los nuevos cambios
- - Por ahora déjalo en 1
- Autor: `Monika After Story`
- - **¡Este campo es obligatorio!**
- - **¡Haz que sea único!**
- - Autor del submod; cámbialo por tu nombre
- Nombre: `Example Submod`
- - **¡Este campo es obligatorio!**
- - **¡Haz que sea único!**
- - El nombre de tu submod; cámbialo por el que quieras usar
- Versión: `0.0.3`
- - **¡Este campo es obligatorio!**
- - Versión de tus submods; debe ser una cadena con 3 enteros separados por `.`
- - Cámbiala por la versión que tenga tu submod; después de actualizar tu submod, sube la versión como consideres adecuado
- - Lee más sobre [versionado semántico](https://semver.org)
- Módulos: `main`
- - **¡Este campo es obligatorio!**
- - Los módulos de tu submod
- - Los módulos son archivos `rpym`/`rpymc` con tu código; deben estar dentro del directorio de tu submod
- - El nombre de un módulo se define por su ruta relativa y su nombre de archivo sin extensión
- - Por ejemplo: `main` significa un `main.rpym` en el directorio raíz de tu submod
- - Otro ejemplo: `utils/logging` significa un `logging.rpym` dentro de una carpeta `utils/` que está dentro del directorio raíz de tu submod
- Descripción: `Este es un ejemplo.`
- - Describe tu submod usando este campo
- Dependencias: `Some Other Submod` con versión de `0.0.8` a `0.1.5`
- - **Esta es una función avanzada**
- - Si tu submod requiere que otro submod esté instalado, puedes especificarlo usando este campo
- - Formato: `dependency_name: [min_version, max_version]`
- Panel de ajustes: `example_submod_screen`
- - **Esta es una función avanzada**
- - Una pantalla que se muestra en el menú de submods (`Esc` -> `Submods`) bajo el nombre de tu submod
- - Esto puede ser útil si quieres añadir algunos ajustes para tu submod o mostrar información extra que no encaje en la descripción
- Actualizaciones de versión: `monika_after_story_example_submod_v0_0_1` a `monika_after_story_example_submod_v0_0_2`
- - **Esta es una función avanzada**
- - Puedes especificar etiquetas para usarlas como "script de actualización" cuando el usuario actualice tu submod
- - Las etiquetas deben seguir el formato `author_submodname_vversion` (fíjate en la `v` extra)
- - En este ejemplo MAS ejecutará `monika_after_story_example_submod_v0_0_1` y luego `monika_after_story_example_submod_v0_0_2` cuando el usuario actualice
- Coautores: lista de otras personas que trabajaron en este submod
- - En este ejemplo será `Example Submod co-author`
- - Este campo es completamente opcional; no tienes que incluir a nadie ni añadir este campo en absoluto
- Prioridad: `0`
- - **Esta es una función avanzada**
- - La prioridad de carga de tu submod; si no estás seguro, no especifiques esto
- - Por defecto, todos los submods tienen prioridad 0; los valores permitidos son enteros en el rango de -999 a 999; más bajo = carga antes, más alto = carga después
- - Si tu submod es una especie de marco, quizá quieras cargarlo antes que otros submods


## Añadir dependencias
De forma hipotética, imaginemos que nuestro submod `Example Submod` requiere código de otro submod (llamado `Required Submod`) para funcionar correctamente.

Para añadir este submod como dependencia del tuyo, queremos añadir una clave y un valor al campo `dependencies`. El formato para esto es el siguiente: `"dependency submod name": ("minimum_version", "maximum_version")`

Por tanto, en este caso la cabecera quedaría así:
```json
{
    "header_version": 1,
    "author": "Monika After Story",
    "name": "Example Submod",
    "version": "0.0.3",
    "description": "This is an example.",
    "modules": [
        "main"
    ],
    "dependencies": {
        "Some Other Submod": ["0.0.8", "0.1.5"],
        "Required Submod": [null, null]
    },
    "settings_pane": "example_submod_screen",
    "version_updates": {
        "monika_after_story_example_submod_v0_0_1": "monika_after_story_example_submod_v0_0_2"
    },
    "coauthors": ["Example Submod co-author"],
    "priority": 0
}
```
Lo cual marca nuestro `Example Submod` como dependiente de un submod llamado `Required Submod`, sin un rango de versiones específico para inicializarse; de lo contrario, MAS no cargará nuestro submod en absoluto hasta que se cumpla la dependencia.

### Aspectos a tener en cuenta:
- Si no hay una versión mínima y/o máxima aplicable, se pueden pasar como `null`.
- Tanto la versión mínima como la máxima se pasarán igual que la versión de tu submod: versionado semántico como cadena.
- Si una dependencia falla, MAS omitirá tu submod durante el proceso de carga y registrará que hay un submod que está fallando la dependencia.

## Añadir un panel de ajustes:
Con submods como estos, no sería ideal saturar los menús principales con ajustes de submods o con formas de llegar a los ajustes de tu submod. Aquí es donde entra en juego el campo `settings_pane`.

Para crear un panel de ajustes, simplemente crea una pantalla que contenga los ajustes de tu submod. Esto se puede hacer igual que cualquier otra inicialización de pantalla en Ren'Py. Para vincularlo a tu submod, pasa el nombre de la pantalla como cadena al campo `settings_pane`.

Por ejemplo, supongamos que hemos creado la siguiente pantalla como pantalla de ajustes:
```renpy
#Don't actually name your screen like this. Use something unique
screen example_submod_screen():
    vbox:
        box_wrap False
        xfill True
        xmaximum 1000

        hbox:
            style_prefix "check"
            box_wrap False

            textbutton _("Switch setting #1") action NullAction()
            textbutton _("Switch setting #2") action NullAction()
            textbutton _("Switch setting #3") action NullAction()
```

Puedes usar descripciones emergentes en los botones de tu panel de ajustes, y se mostrarán en la pantalla principal de submods.
La pantalla de submods ya tiene una descripción emergente (`tooltip`) definida; todo lo que tenemos que hacer es obtener la pantalla, obtener el `tooltip` y ajustar su valor.

Así es como se hace en nuestro ejemplo:
```renpy
screen example_submod_screen():
    python:
        submods_screen = store.renpy.get_screen("submods", "screens")

        if submods_screen:
            _tooltip = submods_screen.scope.get("tooltip", None)
        else:
            _tooltip = None

    vbox:
        box_wrap False
        xfill True
        xmaximum 1000

        hbox:
            style_prefix "check"
            box_wrap False

            if _tooltip:
                textbutton _("Switch setting #1"):
                    action NullAction()
                    hovered SetField(_tooltip, "value", "You will see this text while hovering over the button")
                    unhovered SetField(_tooltip, "value", _tooltip.default)

            else:
                textbutton _("Switch setting #1"):
                    action NullAction()
```
Es una estructura bastante grande, pero te permite cambiar de forma segura las descripciones emergentes de los botones en tu pantalla.

Como puedes ver, tendrás que definir 2 variantes para cada botón:

- Con descripción emergente
- Sin descripción emergente (como alternativa por si no conseguimos obtener la pantalla por algún motivo).

Fíjate en que cambiamos la descripción emergente mediante `SetField`.
En la acción `hovered`, estableceremos la descripción emergente en nuestro valor y, en `unhovered`, la devolveremos a su valor predeterminado usando `_tooltip.default`.

## Crear scripts de actualización:
Crear scripts de actualización es probablemente el aspecto más complejo del marco de submods.

Las etiquetas de script de actualización de submods deben tener un nombre preciso para evitar conflictos debidos a submods con el mismo nombre.

El formato de la etiqueta es el siguiente (campos correspondientes a los valores en la inicialización de `Submod`)
`<author>_<name>_v<version>`

### Aspectos a tener en cuenta:
- Los espacios en las partes `author` y `name` se reemplazarán por _guiones bajos_
- Todos los caracteres de la etiqueta se forzarán a minúsculas
- Los puntos del número de versión se reemplazarán por _guiones bajos_
- El diccionario `version_updates` funciona con un enfoque de `"from_version": "to_version"` y seguirá la cadena presente en el diccionario de actualizaciones (empezando desde el número de versión actual y subiendo hasta arriba)
- Las etiquetas de actualización de submods **deben** aceptar un parámetro llamado `version`, cuyo valor predeterminado es la versión a la que corresponde la etiqueta de actualización
- Los scripts de actualización se ejecutan en **init 10**

Por tanto, con nuestro `Example Submod`, el formato será
`monika_after_story_example_submod_v0_0_1(version="0.0.1")` como nuestra **etiqueta de actualización inicial**.

Si necesitáramos hacer cambios de 0.0.1 a 0.0.2 que deban migrarse, tendríamos las dos etiquetas siguientes:
```renpy
monika_after_story_example_submod_v0_0_1(version="v0_0_1"):
    return

monika_after_story_example_submod_v0_0_2(version="v0_0_2"):
    #Make your changes here
    return
```

Teniendo en cuenta el enfoque `"from_version": "to_version"` para estas actualizaciones, para continuar la cadena si pasáramos de 0.0.2 a 0.0.3 (o a cualquier otra versión), simplemente añadiríamos:

`"monika_after_story_example_submod_v0_0_2": "monika_after_story_example_submod_v0_0_3"` después de la entrada que pusimos arriba.

## Función adicional:
- Como puede haber cambios no disruptivos o quizá quieras añadir una funcionalidad de compatibilidad para el caso en que haya otro submod instalado, puedes usar la función `mas_submod_utils.isSubmodInstalled()`.

### Esta función acepta dos parámetros, uno de ellos obligatorio.
- `name`: El nombre del submod que estás comprobando
- `version`: Un número de versión mínima (por defecto es None. Y, si es None, no se tiene en cuenta al comprobar si un submod está instalado)


# Uso de plugins de funciones:
Aunque las sobrescrituras son útiles, no siempre son ideales en lo referente al mantenimiento entre actualizaciones, o especialmente cuando solo quieres añadir una o dos líneas a una etiqueta o función. Para solucionarlo, se crearon los plugins de funciones.

Este marco te permite registrar funciones que pueden conectarse a cualquier etiqueta que quieras y, además, también a otras funciones, si están preparadas para ejecutarlas.

## Registrar funciones:
Registrar funciones es bastante flexible; los parámetros son los siguientes:

- `key` - La etiqueta (o el nombre de función, como cadena) en la que quieres que se llame a tu función
- `_function` - Un puntero a la función que quieres conectar
- `args` - Argumentos que se pasarán a la función (Por defecto: `[]`)
- `auto_error_handling` - Si el marco de plugins de funciones debe gestionar errores (los registrará y no dejará que MAS se cierre) o no. (Ponlo en `False` si tu función hace un `renpy.call` o un `renpy.jump`) (Por defecto: `True`)
- `priority` - El orden de prioridad en el que deben ejecutarse las funciones. Funciona como los niveles de init: más bajo = antes, más alto = después. (Para funciones que hacen `renpy.call` o `renpy.jump`, usa `mas_submod_utils.JUMP_CALL_PRIORITY`, ya que deberían ejecutarse al final) (Por defecto: `0`)

Hay dos formas de registrar funciones. Una de ellas es usando un `decorador` en la función que quieras registrar.

Ten en cuenta que el enfoque con decorador también elimina la necesidad de pasar manualmente un puntero de función, ya que lo toma directamente de la función a la que está adjunto.

La ventaja de usar este enfoque es que ocupa menos líneas para registrar una función y, además, mejora la *autodocumentación* del código.

Se hace así:
```renpy
init python:
    @store.mas_submod_utils.functionplugin("ch30_minute")
    def example_function():
        """
        This is an example function to demonstrate registering a function plugin using the decorator approach.
        """
        renpy.say(m, "I love you!")
```
Lo cual inicializa un plugin de función en la etiqueta `ch30_minute` que hace que Monika diga "I love you!".

Sin embargo, esto solo funciona si la función que quieres conectar está contenida dentro de los archivos de script de tu submod. Si no es el caso, usamos el segundo enfoque.

Asumiendo la misma `example_function` de arriba:
```renpy
init python:
    store.mas_submod_utils.registerFunction(
        "ch30_minute",
        example_function
    )
```

Lo cual es equivalente al ejemplo anterior.

## Añadir argumentos:
Supongamos que necesitas usar argumentos para tu función; el enfoque es el mismo, salvo que ahora pasamos los argumentos en orden como una `list`. Vamos a cambiar `example_function` para que ahora sea así:
```renpy
init python:
    def example_function(who, what):
        """
        This is an example function to demonstrate registering a function but with arguments
        """
        renpy.say(who, what)
```

Para que esto sea equivalente al último ejemplo, tendríamos que pasar `m` y `"I love you"` como argumentos. A continuación puedes ver ambos enfoques:

Decorador: `@store.mas_submod_utils.functionplugin("ch30_minute", args=[m, "I love you"])`

RegisterFunction():
```renpy
init python:
    store.mas_submod_utils.registerFunction(
        "ch30_minute",
        example_function,
        args=[m, "I love you!"]
    )
```

Con `args` vienen las dos funciones siguientes:
### *store.mas_submod_utils.*`getArgs(key, _function)`:
- Esta función te permite obtener los args de un plugin de función. Solo tienes que pasar la etiqueta/función a la que está asignado y el propio puntero de función, y te devolverá sus args como lista.

### *store.mas_submod_utils.*`setArgs(key, _function, args=[])`:
- Esta función te permite establecer los args de un plugin de función. Solo tienes que pasar la etiqueta/función a la que está asignado, el propio puntero de función y una lista de args nuevos.

También es posible desregistrar un plugin. Solo usa la siguiente función:
### *store.mas_submod_utils.*`unregisterFunction(key, _function)`:
- Esta función te permitirá desregistrar un plugin de función. Solo tienes que pasar la etiqueta/función a la que está asignado y el propio puntero de función, y dejará de estar mapeado a esa etiqueta/función.

Como se mencionó arriba, también es posible mapear plugins de funciones a una *función*.

Este es un caso poco común, pero está contemplado igualmente, aunque no de forma completa en todos los casos. No existe ninguna función en el código de MAS que, por defecto, ejecute plugins de funciones. Si quieres que se ejecuten en una función personalizada tuya, puedes hacerlo añadiendo una línea *store.mas_submod_utils.*`getAndRunFunctions()`.

Esto gestionará automáticamente todas las funciones conectadas a tu función.

### Aspectos a tener en cuenta:
- Los plugins de funciones se pueden registrar en cualquier momento _después_ de init -980
- Los plugins de funciones, por defecto (sin `auto_error_handling` establecido en `False`), gestionarán automáticamente cualquier error en tu función y lo registrarán en `mas_log.log` para evitar que MAS se cierre
- Los plugins de funciones se ejecutan desde el **almacén global**
- Los plugins de funciones se ejecutarán al **inicio** de la etiqueta en la que estén registrados
- Los plugins de funciones se ejecutarán si la etiqueta a la que están vinculados se `call`ea, se `jump`ea o se alcanza por caída

## Globales adicionales
Gracias a la implementación de los plugins de funciones, se añadieron dos nuevas variables globales:

*store.mas_submod_utils.*`current_label`:
- Esta variable guarda la etiqueta *actual* en la que estamos

*store.mas_submod_utils.*`last_label`:
- Esta variable guarda la *última* etiqueta en la que estuvimos
