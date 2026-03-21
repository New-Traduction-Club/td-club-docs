# Índice

* [Introducción](./Adding-Custom-Backgrounds.md#welcome-to-a-complete-newbies-guide-to-the-mas-location-system)
* [Paso 1 - Carpetas y archivos](./Adding-Custom-Backgrounds.md#step-1-folders-and-files-you-need-to-know)
* [Paso 2 - Imágenes y edición](./Adding-Custom-Backgrounds.md#step-2-images-and-editing)
* [Paso 3 - Nombres de imágenes y carpetas](./Adding-Custom-Backgrounds.md#step-3-image-names-and-folders)
* [Paso 4 - Preparación de código](./Adding-Custom-Backgrounds.md#step-4-coding-prep)
* [Paso 5 - IDs de fondos](./Adding-Custom-Backgrounds.md#step-5-background-ids)
* [Paso 6 - MASWeatherMaps](./Adding-Custom-Backgrounds.md#step-6-mas-weather-maps)
* [Paso 7 - MASFilterManager](./Adding-Custom-Backgrounds.md#step-7-mas-filter-manager)
* [Paso 8 - Desbloquear el fondo y los prog points](./Adding-Custom-Backgrounds.md#step-8-unlocking-the-background-and-programming-points)
* [Paso 9 - IDs de imagen](./Adding-Custom-Backgrounds.md#step-9-image-ids)
* [Paso 10 - Finalizar](./Adding-Custom-Backgrounds.md#step-10-finishing-up)
* [Paso 11 - Objetos de decoración](./Adding-Custom-Backgrounds.md#step-11-decoration-objects)

Nota: esta guía está actualizada con la actualización del atardecer, pero aún le falta información sobre cómo crear filtros personalizados.

<a id="welcome-to-a-complete-newbies-guide-to-the-mas-location-system"></a>
### ¡Bienvenido/a a una guía completa para principiantes del sistema de ubicaciones de MAS!
_Esta guía está pensada para quienes tienen poca o ninguna experiencia en programación. Si ya tienes más experiencia, puedes echarle un vistazo rápido y quedarte solo con los pasos que necesites._

**¡Importante!:** Para simplificar, me referiré a la carpeta principal donde se guarda MAS como _DDLC_. La tuya puede llamarse de otra forma (por ejemplo, DDLC-1.1.1-pc), según la versión de DDLC que uses o si la renombraste. Puede tener cualquier nombre, pero en este tutorial la llamaremos así.

> NOTA: Para usuarios de Android (MASL), la carpeta _DDLC_ está definida como _Archivos Internos_.

**Actualización: el selector de ubicaciones se desbloquea con dos condiciones.**
1. Has creado correctamente un archivo .rpy para el/los fondo(s) que quieres usar.
2. Cumples un requisito mínimo de afecto (Enamored, o 400+)

<a id="step-1-folders-and-files-you-need-to-know"></a>
### Paso 1: Carpetas y archivos que necesitas conocer
Este paso es especialmente importante si nunca has añadido submods (complementos creados por la comunidad) ni modificado gráficos en MAS. Para añadir fondos, solo vamos a necesitar entender **dos** rutas de archivos dentro de MAS.

Lo primero que haremos será preparar una carpeta de submod. Aquí es donde guardarás los archivos `.rpy` que hagamos más adelante en este tutorial. Estará dentro de la carpeta `game` de DDLC, así que la ruta quedaría como `DDLC/game/submods`. Debería estar vacía, salvo que ya hayas añadido otros submods.

El segundo directorio que vamos a revisar es `DDLC/game/mod_assets/location`. Si miras dentro de esta carpeta, verás otras carpetas, como una para el spaceroom. No vamos a editar archivos de spaceroom, pero sí volveremos a ellos como referencia y plantilla para nuestras nuevas ubicaciones.


<a id="step-2-images-and-editing"></a>
### Paso 2: Imágenes y edición
Para añadir un fondo personalizado, primero tenemos que preparar las imágenes. Para este tutorial usaré [la habitación de MC, que puedes encontrar en la wiki de DDLC](https://vignette.wikia.nocookie.net/doki-doki-literature-club/images/e/ec/Protagonist_Bedroom.jpg/revision/latest?cb=20180101023322).
Si miras dentro de la carpeta `location/spaceroom`, verás que hay varias versiones para distintas condiciones de tiempo y franjas horarias.
Si quieres, puedes hacer que tu fondo cambie dinámicamente con cualquier tipo de clima del juego. Aun así, las únicas versiones **obligatorias** son una de día y otra de noche. (El atardecer puede resolverse más adelante si no tienes imagen para ello).

Algunas cosas útiles para la edición de imágenes:

- Si tienes cualquier duda sobre los filtros en uso (día, noche, atardecer), sobre cómo crear tu propio filtro o sobre cómo recrear un filtro en un programa de imagen, abre una issue (incidencia en GitHub) y menciona a **@ThePotatoGuy**. Esta guía **NO** cubrirá nada sobre filtros personalizados.
- Asegúrate de que tus imágenes tengan el mismo tamaño/resolución que los archivos de spaceroom (1280x720). No es estrictamente obligatorio, pero una imagen con un tamaño poco habitual puede provocar fallos gráficos o una resolución borrosa.
- Tus imágenes deben guardarse en un formato que Ren'Py pueda usar al crear image tags. (Normalmente, archivos `.png`)

<a id="step-3-image-names-and-folders"></a>
### Paso 3: Nombres de imágenes y carpetas
A partir de este punto, las rutas y los nombres de archivo serán muy importantes. Esto es porque, cuando pasemos a la parte de código, tendremos que decirle a MAS qué archivos usar para los fondos nuevos.

Ahora volvemos al directorio `DDLC/game/mod_assets/location`. Después, crearemos una carpeta con el nombre de la ubicación que quieras usar. Dentro de esa carpeta, añadiremos tus variantes de día y de noche (y otros climas, si los tienes).
Luego haremos que los nombres coincidan con los archivos de la carpeta _**spaceroom**_.

**Por ejemplo, la imagen nocturna por defecto de spaceroom se llama `spaceroom-n.png`.
Entonces, el archivo de mi dormitorio sería `bedroom-n.png`.**

Al terminar esto, yo tendría `DDLC/game/mod_assets/location/bedroom`, con `bedroom.png` y `bedroom-n.png` dentro.

<a id="step-4-coding-prep"></a>
### Paso 4: Preparación de código

Aquí es donde empezaremos la parte de código para añadir fondos. Te conviene crear un archivo `.rpy` en el programa que prefieras.
Ese archivo irá en tu carpeta `DDLC/game/submods` cuando esté terminado. Por ahora puede estar totalmente en blanco.
Primero vamos a echar un vistazo a `zz_backgrounds.rpy`, que ya existe en MAS. Para encontrar la sección donde se definen los fondos del juego, busca `START: bg defs`. Vamos a usar el código de spaceroom como plantilla y a construir nuestro fondo de la misma forma.
Hay bastante código, pero lo iremos dividiendo en partes fáciles de entender.

<a id="step-5-background-ids"></a>
### Paso 5: IDs de fondos
El primer paso es sencillo. En el fondo spaceroom podemos ver:

```renpy
init -1 python: 
    #Default spaceroom
    mas_background_def = MASFilterableBackground(
        # ID
        "spaceroom",
        "Spaceroom",
```
**Nota: cualquier línea que empiece con `#` es un comentario y no afecta al código. Puedes borrarlas o dejarlas, como prefieras.**
Este bloque de código es donde pondrás el nombre y el ID de tu fondo.
`mas_background_def = MASFilterableBackground(` básicamente está ahí para indicarle al juego que este fondo funciona con el framework de filtros (sistema que aplica efectos visuales según el contexto). Te conviene dejar esa línea tal cual.
Estos dos valores pueden ser iguales o distintos, pero la primera línea (`"spaceroom",`) debe ser única respecto a otros fondos de MAS (así que no llames a otro fondo `"spaceroom"`).
Para evitar que tu submod entre en conflicto con futuras actualizaciones, quizá te convenga añadir algo como `"custom"` o `"submod"` a tu ID.

La segunda línea es cómo aparecerá la sala en el diálogo del selector de fondos, incluyendo mayúsculas. Esta sí puede repetirse, así que puedes poner el nombre que prefieras.

Para seguir con nuestro ejemplo de la habitación de MC, la llamaremos “Bedroom”, así que en nuestro .rpy debería quedar algo como esto:

```renpy
init -1 python: 
    mas_background_def = MASFilterableBackground(
        "submodbedroom",
        "Bedroom",
```

<a id="step-6-mas-weather-maps"></a>
### Paso 6: MASWeatherMaps

A continuación, en nuestra plantilla veremos un bloque de código bastante grande. Aunque sea largo, es fácil de entender.

```renpy
        # mapping of filters to MASWeatherMaps
        MASFilterWeatherMap(
            day=MASWeatherMap({
                store.mas_weather.PRECIP_TYPE_DEF: "monika_day_room",
                store.mas_weather.PRECIP_TYPE_RAIN: "monika_rain_room",
                store.mas_weather.PRECIP_TYPE_OVERCAST: "monika_rain_room",
                store.mas_weather.PRECIP_TYPE_SNOW: "monika_snow_room_day",
            }),
            night=MASWeatherMap({
                store.mas_weather.PRECIP_TYPE_DEF: "monika_room",
                store.mas_weather.PRECIP_TYPE_SNOW: "monika_snow_room_night",
            }),
            sunset=MASWeatherMap({
                store.mas_weather.PRECIP_TYPE_DEF: "monika_ss_room",
                store.mas_weather.PRECIP_TYPE_RAIN: "monika_rain_room_ss",
                store.mas_weather.PRECIP_TYPE_OVERCAST: "monika_rain_room_ss",
                store.mas_weather.PRECIP_TYPE_SNOW: "monika_snow_room_ss",
            }),
        ),
```

Si lo desglosamos, verás que está separado por horas del día y por clima.
Aquí se asigna un ID de imagen a cada tipo de clima para el que tengas una imagen propia.
El ID puede llamarse como quieras y no tiene por qué coincidir con el nombre del archivo de imagen, pero debe ser único. (Igual que con el ID de sala, quizá te convenga incluir algo como `"submod"` o `"custom"` en el nombre para evitar solapamientos si más adelante se añaden fondos al juego base).

Si para el día o la noche no tienes una imagen específica de un clima, y no le asignas ID, usará por defecto la imagen de `TYPE_DEF`.
Así que, si solo tienes imágenes de clima por defecto, puedes omitir las líneas de climas alternativos.
En mi ejemplo del dormitorio, esto quedaría más o menos así.

```renpy
        MASFilterWeatherMap(
            day=MASWeatherMap({
                store.mas_weather.PRECIP_TYPE_DEF: "submod_day_mcbedroom",
            }),
            night=MASWeatherMap({
                store.mas_weather.PRECIP_TYPE_DEF: "submod_night_mcbedroom",
            }),
            sunset=MASWeatherMap({
                store.mas_weather.PRECIP_TYPE_DEF: "submod_ss_mcbedroom",
            }),
        ),
```

Si quieres usar la misma imagen para varios climas _distintos del predeterminado_ (por ejemplo, usar la misma imagen para Rain y Overcast), tendrás que usar el mismo nombre de ID para ambos. (Como se ve en la plantilla de spaceroom con rain y overcast en atardecer).

En este punto, nuestro archivo se verá así.

```renpy
init -1 python: 
    mas_background_def = MASFilterableBackground(
        "submodbedroom",
        "Bedroom",
        MASFilterWeatherMap(
            day=MASWeatherMap({
                store.mas_weather.PRECIP_TYPE_DEF: "submod_day_mcbedroom",
            }),
            night=MASWeatherMap({
                store.mas_weather.PRECIP_TYPE_DEF: "submod_night_mcbedroom",
            }),
            sunset=MASWeatherMap({
                store.mas_weather.PRECIP_TYPE_DEF: "submod_ss_mcbedroom",
            }),
        ),
```

<a id="step-7-mas-filter-manager"></a>
### Paso 7: MASFilterManager

```renpy
        # filter manager
        MASBackgroundFilterManager(
            MASBackgroundFilterChunk(
                False,
                None,
                MASBackgroundFilterSlice.cachecreate(
                    store.mas_sprites.FLT_NIGHT,
                    60
                )
            ),
            MASBackgroundFilterChunk(
                True,
                None,
                MASBackgroundFilterSlice.cachecreate(
                    store.mas_sprites.FLT_SUNSET,
                    60,
                    30*60,
                    10,
                ),
                MASBackgroundFilterSlice.cachecreate(
                    store.mas_sprites.FLT_DAY,
                    60
                ),
                MASBackgroundFilterSlice.cachecreate(
                    store.mas_sprites.FLT_SUNSET,
                    60,
                    30*60,
                    10,
                ),
            ),
            MASBackgroundFilterChunk(
                False,
                None,
                MASBackgroundFilterSlice.cachecreate(
                    store.mas_sprites.FLT_NIGHT,
                    60
                )
            )
        ),
```

El `MASBackgroundFilterManager` determina qué filtro debe mostrarse en cada momento. Este objeto se compone de 3 objetos `MASBackgroundFilterChunk`:

1. El primer `FilterChunk` representa el tiempo entre medianoche y la hora de amanecer configurada por el usuario.
2. El segundo `FilterChunk` representa el tiempo entre el amanecer y el atardecer configurados por el usuario.
3. El tercer `FilterChunk` representa el tiempo entre el atardecer configurado por el usuario y la siguiente medianoche.

Cada `FilterChunk` puede contener una cantidad arbitraria de objetos `MASBackgroundFilterSlice`, lo que te permite crear casi cualquier patrón de filtros. Tampoco necesitas preocuparte por horas exactas, porque el `FilterManager` organizará los filtros según el tiempo disponible en función de las horas de sol configuradas por el usuario.

_Estructura de `MASBackgroundFilterManager`_
```renpy
MASBackgroundFilterManager(
    <FilterChunk object>, # FilterChunk that represents time between midnight and user-set sunrise
    <FilterChunk object>, # FilterChunk that represents time between user-set sunrise and user-set sunset
    <FilterChunk object>, # FilterChunk that represents time between user-set sunset and the next midnight
    <prog point> # OPTIONAL - allows you to run code between chunk transitions. May not always run. See the MASBackgroundFilterManager's constructor documentation for more info (in `zz_backgrounds.rpy`)
)
```

_Estructura de `MASBackgroundFilterChunk`_
```renpy
MASBackgroundFilterChunk(
    <boolean>, # pass True if this is a "day" chunk, False if this is a "night" chunk. This is important for determining appropriate dialogue as well as UI. In general, setting the 1st and 3rd chunks as night chunks and the second chunk as a day chunk is sufficient.
    <prog point>, # allows you to run code between FilterSlice transitions. May not always run. Pass in None if you don't want to run any progpoints. See the MASBackgroundFilterChunk's constructor documentation for more info (in `zz_backgrounds.rpy`)
    *slices # arbitrary number of FilterSlice objects, ordered in the exact order the filters should be shown during a time chunk.
)
```

_Estructura de `MASBackgroundFilterSlice`_
```renpy
MASBackgroundFilterSlice.cachecreate( # NOTE: this function caches slices so we don't make extra ones if a slice is identical. Always use this.
    <name>, # the filter to associate with this time slice
    <minlength>, # the shortest number of seconds this filter can exist for
    <maxlength>, # OPTIONAL - the maxiumum number of seconds this filter can exist for. If not set, then this FilterSlice is unbounded and can have as much length as needed
    <priority> # OPTIONAL - how important this slice is from 1-10. Larger numbers are more important. If not set, then this FilterSlice has a priority of 10.
)
```

El `FilterManager` ajustará el tamaño de los `FilterSlice` hasta cubrir todo el `FilterChunk`. Por eso las únicas opciones disponibles para `FilterSlice` son las longitudes mínima y máxima, que en la práctica limitan cuánto tiempo puede mostrarse un filtro. Si hay demasiados `FilterSlice` para un `FilterChunk`, el `FilterManager` omitirá los de menor prioridad.

Si estás copiando los filtros del spaceroom vanilla, tu .rpy quedará más o menos así.

```renpy
init -1 python: 
    mas_background_def = MASFilterableBackground(
        "submodbedroom",
        "Bedroom",
        MASFilterWeatherMap(
            day=MASWeatherMap({
                store.mas_weather.PRECIP_TYPE_DEF: "submod_day_mcbedroom",
            }),
            night=MASWeatherMap({
                store.mas_weather.PRECIP_TYPE_DEF: "submod_night_mcbedroom",
            }),
            sunset=MASWeatherMap({
                store.mas_weather.PRECIP_TYPE_DEF: "submod_ss_mcbedroom",
            }),
        ),
        MASBackgroundFilterManager(
            MASBackgroundFilterChunk(
                False,
                None,
                MASBackgroundFilterSlice.cachecreate(
                    store.mas_sprites.FLT_NIGHT,
                    60
                )
            ),
            MASBackgroundFilterChunk(
                True,
                None,
                MASBackgroundFilterSlice.cachecreate(
                    store.mas_sprites.FLT_SUNSET,
                    60,
                    30*60,
                    10,
                ),
                MASBackgroundFilterSlice.cachecreate(
                    store.mas_sprites.FLT_DAY,
                    60
                ),
                MASBackgroundFilterSlice.cachecreate(
                    store.mas_sprites.FLT_SUNSET,
                    60,
                    30*60,
                    10,
                ),
            ),
            MASBackgroundFilterChunk(
                False,
                None,
                MASBackgroundFilterSlice.cachecreate(
                    store.mas_sprites.FLT_NIGHT,
                    60
                )
            )
        ),
```

<a id="step-8-unlocking-the-background-and-programming-points"></a>
### Paso 8: Desbloquear el fondo y los prog points (puntos de programación)

```renpy
        unlocked=True,
        entry_pp=store.mas_background._def_background_entry,
        exit_pp=store.mas_background._def_background_exit,
    )
```

Debemos asegurarnos de que `unlocked` esté en `True`, para que tu fondo aparezca en el selector.
`entry_pp` y `exit_pp` pueden usarse para personalizaciones avanzadas, como bloquear o desbloquear temas específicos de este fondo. No se cubrirán en esta guía y, para un fondo básico, puedes dejarlos como están.

Esta también es la sección en la que puedes configurar varias variables más. `hide_calendar = True` ocultará el calendario en este fondo. `disable_progressive = True` evitará que el clima cambie por sí solo. `hide_masks = True` desactivará el clima animado del exterior. Si tu fondo tiene ventana, te conviene poner `hide_masks = False`.

<a id="step-9-image-ids"></a>
### Paso 9: IDs de imagen
¡Ya casi terminamos! Solo nos queda revisar un último bloque de código.

```renpy
#START: Image definitions
#Spaceroom
image monika_day_room = "mod_assets/location/spaceroom/spaceroom.png"
image monika_room = "mod_assets/location/spaceroom/spaceroom-n.png"
image monika_ss_room = MASFilteredSprite(
    store.mas_sprites.FLT_SUNSET,
    "mod_assets/location/spaceroom/spaceroom.png"
)
```

La mayor parte de esto se mantendrá igual, pero debemos fijarnos en dónde empiezan las definiciones de imagen.
Como ves, ahora vamos a decirle a MAS dónde encontrar cada imagen a la que le asignamos un ID en el Paso 6.
También puedes ver que no necesitamos obligatoriamente una imagen de atardecer ya filtrada para sunset. Puedes usar directamente la imagen de día con el código de `MASFilteredSprite`.

```renpy
image submod_day_mcbedroom = "mod_assets/location/mcbedroom/mcbedroom.png"
image submod_night_mcbedroom = "mod_assets/location/mcbedroom/mcbedroom-n.png"
image submod_ss_mcbedroom = MASFilteredSprite(
    store.mas_sprites.FLT_SUNSET,
    "mod_assets/location/mcbedroom/mcbedroom.png"
)
```

<a id="step-10-finishing-up"></a>
### Paso 10: ¡Finalizando!
Por último, revisaremos el archivo y comprobaremos si hay errores.

```renpy
init -1 python: 
    mas_background_def = MASFilterableBackground(
        "submodbedroom",
        "Bedroom",
        MASFilterWeatherMap(
            day=MASWeatherMap({
                store.mas_weather.PRECIP_TYPE_DEF: "submod_day_mcbedroom",
            }),
            night=MASWeatherMap({
                store.mas_weather.PRECIP_TYPE_DEF: "submod_night_mcbedroom",
            }),
            sunset=MASWeatherMap({
                store.mas_weather.PRECIP_TYPE_DEF: "submod_ss_mcbedroom",
            }),
        ),
        MASBackgroundFilterManager(
            MASBackgroundFilterChunk(
                False,
                None,
                MASBackgroundFilterSlice.cachecreate(
                    store.mas_sprites.FLT_NIGHT,
                    60
                )
            ),
            MASBackgroundFilterChunk(
                True,
                None,
                MASBackgroundFilterSlice.cachecreate(
                    store.mas_sprites.FLT_SUNSET,
                    60,
                    30*60,
                    10,
                ),
                MASBackgroundFilterSlice.cachecreate(
                    store.mas_sprites.FLT_DAY,
                    60
                ),
                MASBackgroundFilterSlice.cachecreate(
                    store.mas_sprites.FLT_SUNSET,
                    60,
                    30*60,
                    10,
                ),
            ),
            MASBackgroundFilterChunk(
                False,
                None,
                MASBackgroundFilterSlice.cachecreate(
                    store.mas_sprites.FLT_NIGHT,
                    60
                )
            )
        ),
        unlocked=True,
        entry_pp=store.mas_background._def_background_entry,
        exit_pp=store.mas_background._def_background_exit,
    )

    #Now load data
    store.mas_background.loadMBGData()

image submod_day_mcbedroom = "mod_assets/location/mcbedroom/mcbedroom.png"
image submod_night_mcbedroom = "mod_assets/location/mcbedroom/mcbedroom-n.png"
image submod_ss_mcbedroom = MASFilteredSprite(
    store.mas_sprites.FLT_SUNSET,
    "mod_assets/location/mcbedroom/mcbedroom.png"
)
```


Asegúrate de guardar el archivo como `.rpy` y ya podrás ponerlo en tu carpeta de MAS.
Cuando inicies MAS la próxima vez, deberías tener una opción de diálogo en “Hey, Monika… > Ubicación”.

¡Disfruta de tus nuevos fondos!

<a id="step-11-decoration-objects"></a>
### Paso 11 - Objetos de decoración

Si quieres mostrar objetos de decoración (como cuando decoramos el spaceroom en días festivos), tendrás que registrar las decoraciones para tus fondos. Consulta [el framework Deco para fondos](./The-Deco-Framework-for-Backgrounds.md) para ver cómo hacerlo.
