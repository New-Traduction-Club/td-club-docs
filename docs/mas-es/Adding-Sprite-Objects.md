La versión 0.9.4 introdujo la adición de sprites mediante archivos JSON.

# Índice
1. [Instalar paquetes de sprites/arte](./Adding-Sprite-Objects.md#instalar-sprite-packs)
2. [Usar paquetes de sprites/arte en el juego](./Adding-Sprite-Objects.md#usar-sprite-packs-en-el-juego)
3. [Crear paquetes de sprites/arte](./Adding-Sprite-Objects.md#crear-sprite-packs)
4. [Formatos JSON](./Adding-Sprite-Objects.md#formato-json)
5. [Explicación de campos JSON](./Adding-Sprite-Objects.md#explicacion-de-objetos)
6. [Ubicaciones de archivos](./Adding-Sprite-Objects.md#ubicaciones-de-archivos)
7. [Puntos prog](./Adding-Sprite-Objects.md#puntos-prog)
8. [Reacciones de regalos](./Adding-Sprite-Objects.md#reacciones-de-regalos)
9. [Exprops disponibles](./Adding-Sprite-Objects.md#exprops-disponibles)
10. [ACSTemplates](./Adding-Sprite-Objects.md#acstemplates)
11. [Historial de versiones](./Adding-Sprite-Objects.md#historial-de-versiones)

<a id="instalar-sprite-packs"></a>
# Instalar paquetes de sprites

Instalar estos paquetes de sprites en tu mod se hace igual que cuando instalaste el mod o cuando aplicas actualizaciones manuales.

1. Descarga el archivo ZIP del paquete de sprites desde la [página de lanzamientos](http://www.monikaafterstory.com/releases.html) de MAS.

2. El archivo ZIP contendrá carpetas con los nombres de los paquetes de sprites, y dentro de cada una habrá una carpeta llamada `mod_assets`. Solo tienes que copiar la carpeta `mod_assets` del paquete de sprites que quieras instalar **con MAS cerrado** y pegarla en la carpeta `game`, que está en el directorio raíz de tu instalación de MAS.
     * En una instalación de Steam en cualquier sistema operativo, accede al directorio base haciendo clic derecho en el juego Doki Doki Literature Club en tu biblioteca de Steam, pulsa la opción `Properties`, luego la pestaña `Local Files` y después `Browse Local Files`.
     * En Windows sin Steam, es la carpeta desde la que inicias el juego.
     * En Mac sin Steam, dentro de tu instalación de MAS haz clic derecho en `DDLC.app` (puede que solo aparezca como `DDLC`) y pulsa `Show package Contents`; después navega a `Contents/Resources/autorun/`
     * En Android (MASL), entra a _Explorar Archivos Internos_.

Vídeo de ejemplo de la instalación [aquí](https://www.youtube.com/watch?v=bjJ0U8l1m8c)

## Solución de problemas de instalación
  
1. ¿Copiaste la carpeta `mod_assets` del paquete de sprites que querías instalar dentro de `game/`? Es decir, **no** debería haber una carpeta como `author-spritepackname` dentro de `game/` ni de `mod_assets/`.
    1. **SÍ** - elimina la carpeta `author-spritepackname` de `game/` o `mod_assets/` y copia la carpeta `mod_assets` del paquete de sprites en tu `game/`; vuelve a intentar regalar.
    2. **NO** - continúa con el paso 2.
2. ¿`log/spj.log` muestra los sprites que querías regalar? (Consulta [aquí](./FAQ.md#how-to-view-your-log-files) si no sabes cómo revisar los logs)
    1. **SÍ** - continúa con el paso 3.
    2. **NO** - verifica que has instalado correctamente el contenido de un paquete de sprites en `game/` y, si lo instalaste con MAS en ejecución, despídete y vuelve a abrir el juego.
3. ¿`log/spj.log` contiene alguna línea con `ERROR`? Si ya lo hiciste y los sprites siguen sin aparecer en el registro, ve al paso 6.
    1. **SÍ** - verifica que has instalado correctamente el contenido de un paquete de sprites en `game/` e inténtalo de nuevo. Si ya lo hiciste y siguen apareciendo errores, ve al paso 6.
    2. **NO** - continúa con el paso 4.
4. ¿Estás añadiendo un paquete de sprites de peinados?
    1. **SÍ** - los peinados no se pueden regalar; deberían estar ya desbloqueados, salvo que quien haya creado el paquete de sprites use código personalizado para desbloquearlos. Puedes encontrar los peinados desbloqueados en `Hey, Monika... > Appearance... > Can you change your hairstyle?`
    2. **NO** - continúa con el paso 5.
5. ¿Copiaste los archivos de la carpeta `gifts/` en tu carpeta `characters/`?
    1. **SÍ** - continúa con el paso 6.
    2. **NO** - copia los archivos de la carpeta `gifts/` en tu carpeta `characters/`.
6. Crea una incidencia e incluye lo siguiente:
    * nombre del paquete de sprites que intentas instalar
    * nombre del regalo que intentas dar
    * `log/spj.log` 

<a id="usar-sprite-packs-en-el-juego"></a>
# Usar paquetes de sprites en el juego

Cada sprite de un paquete tiene un `giftname` asociado. Los archivos con los `giftname` adecuados están en la carpeta `gifts/` del paquete de sprites. **NOTA: no todos los objetos de sprite se pueden desbloquear de esta manera.**

<a id="crear-sprite-packs"></a>
# Crear paquetes de sprites

Para crear paquetes de sprites solo hacen falta dos cosas: arte y JSON para describir cada sprite.

El arte debe estar en el tamaño adecuado de 1280x850 (salvo la miniatura). Consulta [Ubicaciones de archivos](./Adding-Sprite-Objects.md#ubicaciones-de-archivos) para saber dónde colocarlo.

Los JSON deben seguir el formato que aparece más abajo. De nuevo, consulta [Ubicaciones de archivos](./Adding-Sprite-Objects.md#ubicaciones-de-archivos) para saber dónde colocar el JSON.

Y no lo olvides: `log/spj.log` es tu mejor aliado para depurar.

## Enviar un paquete de sprites:
Requisitos para el envío:

* Incluye [JSON](./Adding-Sprite-Objects.md#formato-json) para los sprites.
* La [estructura de carpetas del paquete de sprites](./Adding-Sprite-Objects.md#ubicaciones-de-archivos) es correcta.
* **Debe** cumplirse una de las siguientes condiciones:
    * el arte lo has creado tú
    * el arte lo has encargado tú
    * el arte te pertenece
    * la persona creadora del arte te ha dado permiso explícito para crear un paquete de sprites

**Los paquetes de sprites enviados a la incidencia de sprite packs (#3765) no son aptos para añadirse a los paquetes de sprites oficiales.** Para enviar algo a los paquetes de sprites oficiales, crea una incidencia. Ten en cuenta que tenemos la última palabra sobre el uso de sprites incluidos en los paquetes de sprites oficiales.

# Formato JSON

<a id="acs-regular"></a>
## ACS (normal)
```json
{
    "version": 4,
    "type": 0,
    "name": "id-of-sprite",
    "img_sit": "base_filename_without_extension",
    "pose_map": {
        "default": "0",
        "l_default": "5",
        "use_reg_for_l": false,
        "p1": "1",
        "p2": "2",
        "p3": "3",
        "p4": "4",
        "p5": "5",
        "p6": "6",
        "p7": "7"
    },
    "stay_on_start": true,
    "ex_props": {
        "propname": "propvalue"
    },
    "select_info": {
        "display_name": "User Friendly Name",
        "thumb": "thumbnail_filename_without_extension",
        "group": "id-of-selection-group",
        "visible_when_locked": false,
        "select_dlg": [
            "list of dialogue to show when selected"
        ]
    },
    "giftname": "gift_filename_without_extension",
    "dryrun": false,
    "rec_layer": 3,
    "priority": 10,
    "acs_type": "accessory-type",
    "mux_type": [
        "list-of-mutually-exclusive-types"
    ],
    "dlg_desc": "user-friendly accessory name",
    "dlg_plural": false,
    "keep_on_desk": false
}
```

<a id="acs-split"></a>
## ACS (separado)
```json
{
    "version": 4,
    "type": 0,
    "name": "id-of-sprite",
    "img_sit": "base_filename_without_extension",
    "pose_map": {
        "default": "0",
        "l_default": "5",
        "use_reg_for_l": false,
        "p1": "1",
        "p2": "2",
        "p3": "3",
        "p4": "4",
        "p5": "5",
        "p6": "6",
        "p7": "7"
    },
    "stay_on_start": true,
    "ex_props": {
        "propname": "propvalue"
    },
    "select_info": {
        "display_name": "User Friendly Name",
        "thumb": "thumbnail_filename_without_extension",
        "group": "id-of-selection-group",
        "visible_when_locked": false,
        "select_dlg": [
            "list of dialogue to show when selected"
        ]
    },
    "giftname": "gift_filename_without_extension",
    "dryrun": false,
    "rec_layer": 3,
    "priority": 10,
    "acs_type": "accessory-type",
    "mux_type": [
        "list-of-mutually-exclusive-types"
    ],
    "arm_split": {
        "default": "0",
        "l_default": "5",
        "use_reg_for_l": true,
        "p1": "0",
        "p2": "",
        "p3": "5",
        "p4": "10",
        "p5": "5^10",
        "p6": "*",
        "p7": "*"
    },
    "dlg_desc": "user-friendly accessory name",
    "dlg_plural": false,
    "keep_on_desk": false
}
```

<a id="hair"></a>
## Peinado
```json
{
    "version": 4,
    "type": 1,
    "name": "id-of-sprite",
    "img_sit": "base_filename_without_extension",
    "pose_map": {
        "mpm_type": 0,
        "default": true,
        "l_default": false,
        "use_reg_for_l": false,
        "p1": true,
        "p2": false,
        "p3": true,
        "p4": false,
        "p5": true,
        "p6": false,
        "p7": false
    },
    "mid_hair_map": {
        "mpm_type": 0,
        "default": false,
        "l_default": false
    },
    "stay_on_start": true,
    "ex_props": {
        "propname": "propvalue"
    },
    "select_info": {
        "display_name": "User Friendly Name",
        "thumb": "thumbnail_filename_without_extension",
        "group": "id-of-selection-group",
        "visible_when_locked": true,
        "select_dlg": [
            "list of dialogue to show when selected"
        ]
    },
    "unlock": true,
    "dryrun": false
}
```

<a id="clothes"></a>
## Ropa
```json
{
    "version": 4,
    "type": 2,
    "name": "id-of-sprite",
    "img_sit": "base_filename_without_extension",
    "pose_map": {
        "mpm_type": 1,
        "default": "steepling",
        "l_default": "def|def",
        "use_reg_for_l": true,
        "p1": "steepling",
        "p2": "crossed",
        "p3": "restleftpointright",
        "p4": "pointright",
        "p5": "steepling",
        "p6": "down"
    },
    "stay_on_start": true,
    "ex_props": {
        "propname": "propvalue"
    },
    "select_info": {
        "display_name": "User Friendly Name",
        "thumb": "thumbnail_filename_without_extension",
        "group": "id-of-selection-group",
        "visible_when_locked": true,
        "hover_dlg": [
            "list of dialogue to show when hovered"
        ],
        "select_dlg": [
            "list of dialogue to show when selected"
        ],
    },
    "giftname": "gift_filename_without_extension",
    "dryrun": false,
    "hair_map": {
        "all": "def",
        "bun": "def"
    },
    "pose_arms": {
        "crossed": {
            "tag": "crossed",
            "layers": "5^10"
        },
        "left-down": {
            "tag": "down",
            "layers": "0"
        },
        "left-rest": {
            "tag": "rest",
            "layers": "10"
        },
        "right-down": {
            "tag": "down",
            "layers": "0"
        },
        "right-point": {
            "tag": "point",
            "layers": "0"
        },
        "right-restpoint": {
            "tag": "restpoint",
            "layers": "10"
        },
        "steepling": {
            "tag": "steepling",
            "layers": "10"
        },
        "def|left-def": {
            "tag": "def",
            "layers": "10"
        },
        "def|right-def": {
            "tag": "def",
            "layers": "5^10"
        }
    },
    "outfit_hair": "hair-sprite-ID",
    "outfit_acs": [
        "acs-ID",
        "another-acs-ID"
    ]
}
```

<a id="highlights"></a>
## Resaltados
Las capas de resaltado son una forma de añadir capas a un sprite que no se verán afectadas por el sistema de filtrado. Por ejemplo, pueden usarse para añadir brillo a un sprite durante la noche.

Aquí tienes un ejemplo simplificado para añadir capas de resaltado a un ACS por la noche (solo se muestran las propiedades relevantes).
```json
{
    "version": 4,
    "type": 0,
    "name": "glowingacs",
    "img_sit": "glowingacs",
    "pose_map": {
        "default": "0",
        "l_default": "5",
        "p1": "0",
        "p2": "1",
        "p3": "0",
        "p4": "2",
        "p5": "5",
        "p6": "0",
        "p7": "1"
    },
    "highlight": {
        "mapping": {
            "0": {
                "night": "0"
            },
            "1": {
                "night": "1"
            },
            "2": {
                "night": "2"
            },
            "5": {
                "night": "5"
            }
        }
    }
}
```

Este ejemplo asume lo siguiente:

* El ACS tiene imágenes que usan los códigos de pose 0, 1, 2 y 5.
* El ACS tiene capas de resaltado para esas imágenes.

Los archivos y rutas resultantes para que esto coincida con este JSON son:

* `glowingacs/0.png`
* `glowingacs/0-h0.png` - capa de resaltado que se aplica a cualquier pose que use el código de pose `0`
* `glowingacs/1.png`
* `glowingacs/1-h1.png` - capa de resaltado que se aplica a cualquier pose que use el código de pose `1`
* `glowingacs/2.png`
* `glowingacs/2-h2.png` - capa de resaltado que se aplica a cualquier pose que use el código de pose `2`
* `glowingacs/5.png`
* `glowingacs/5-h5.png` - capa de resaltado que se aplica a cualquier pose que use el código de pose `5`

**El código de resaltado NO tiene que coincidir con el código de pose.** En el ejemplo se usa el mismo valor por comodidad organizativa. En general, las capas de resaltado solo necesitan llevar el sufijo `-h#`, donde `#` puede ser cualquier cadena.

Además, `Clothes` y `Hair` tienen claves de mapeo distintas a las de ACS. Encontrarás más explicación en la sección [Objeto `Highlight`](#highlight-object).

Para saber dónde colocar la propiedad `highlight`, consulta la sección [Explicación de objetos](#object-explanation) más abajo.

<a id="object-explanation"></a>
<a id="explicacion-de-objetos"></a>
## Explicación de objetos:

### Pares nombre/valor comunes:
Estas propiedades se aplican a todos los objetos de sprite.

* `version`: (`int`) versión de este sprite
    * **obligatorio**
    * usa la versión 4 si las imágenes siguen el formato basado en carpetas; consulta [Ubicaciones de archivos de la versión 4](#version-4-file-locations-v01216)
        * **Usa este formato en adelante (v0.12.16+); es mucho mejor para la organización.**
    * usa la versión 3 si las imágenes siguen el formato basado en nombre de archivo; consulta [Ubicaciones de archivos de la versión 3](#version-3-file-locations-v0110-v01215)
        * solo es compatible en v0.11.0+
* `type`: (`int`) tipo de este sprite
    * **obligatorio**
    * Debe ser uno de los siguientes valores:
        * 0 - ACS
        * 1 - `Hair`
        * 2 - `Clothes`
* `name`: (`string`) nombre de este sprite
    * **obligatorio**
    * **debe ser único dentro del tipo de sprite**
    * Se usa como identificador de este sprite.
* `img_sit`: (`string`) nombre de archivo para la posición sentada de este sprite
    * **obligatorio**
    * **No** incluyas la extensión del archivo.
    * **No** incluyas la ruta del archivo.
* `pose_map`: (`object`) [Objeto PoseMap](#posemap-object)
    * **obligatorio**
    * su uso varía según el tipo de sprite. Consulta [aquí](#posemap-object) para más información.
* `stay_on_start`: (`boolean`) determina si Monika debe seguir llevando el objeto de sprite tras reiniciar
    * _opcional_
    * `True` permite que Monika siga llevando el sprite tras reiniciar. `False` elimina el sprite al salir.
    * Valor por defecto: `false`
* `ex_props`: (`object`) diccionario de propiedades arbitrarias
    * _opcional_
    * Permite asignar propiedades arbitrarias a este objeto de sprite.
    * Es como ponerle "etiquetas" al objeto de sprite.
    * **Las claves deben ser cadenas (`string`).**
    * **Los valores deben ser `string`, `int` o `bool`.**
    * [Exprops disponibles](./Adding-Sprite-Objects.md#available-exprops)
    * Valor por defecto: `objeto vacío`
* `select_info`: (`object`) [Objeto Selectable](#selectable-object)
    * _opcional_
    * Permite que el objeto de sprite sea seleccionable mediante un selector. Consulta [aquí](#selectable-object) para más información.
    * Valor por defecto: `objeto vacío`
* `highlight`: (`object`) [Objeto `Highlight`](#highlight-object) o [Objeto `HighlightSplit`](#highlightsplit-object) si es un ACS dividido (`Split ACS`)
    * _opcional_
    * los resaltados son capas añadidas a sprites que ignoran el sistema de filtrado
    * los ACS con `arm_split` configurado deben usar [objetos `HighlightSplit`](#highlightsplit-object)
* `dryrun`: (`any`) clave de metadatos que habilita el modo dryrun
    * _opcional_
    * Si se proporciona, el objeto de sprite **no** se añadirá formalmente a la base de datos, pero se comprobará en busca de errores/advertencias (es decir, una ejecución de prueba).
    * El valor no importa.

<a id="acs-specific"></a>
### Específico de ACS
Estas propiedades son solo para sprites ACS.

* `rec_layer`: (`int`) capa deseada para este ACS
    * _opcional_
    * Debe ser uno de los siguientes valores:
        * 0 - antes del cuerpo (`PRE_ACS`)
        * 1 - entre las expresiones faciales y los brazos (`MID_ACS`)
        * 2 - después de los brazos (`PST_ACS`)
        * 3 - entre el pelo trasero y el cuerpo (`BBH_ACS`)
        * 4 - entre el cuerpo y el pelo delantero (`BFH_ACS`)
        * 5 - entre el pelo delantero y las expresiones faciales (`AFH_ACS`)
        * 6 - entre el cuerpo y los brazos traseros (`BBA_ACS`)
        * 7 - entre los brazos intermedios y el pecho (`MAB_ACS`)
        * 8 - entre el cuerpo base y la ropa (`BSE_ACS`)
        * 9 - entre los brazos base y la ropa (`ASE_ACS`)
        * 10 - entre el pelo medio y la mesa (`BAT_ACS`)
        * 11 - entre los brazos intermedios y la mesa (`MAT_ACS`)
        * 12 - entre los brazos traseros y el pelo medio (`BMH_ACS`)
        * 13 - entre el pelo medio y la cabeza (`MMH_ACS`)
    * Esto hará que el ACS se renderice solo en esta capa.
    * Valor por defecto: `2` (`PST_ACS`)
* `priority`: (`int`) prioridad de renderizado
    * _opcional_
    * Los valores más bajos se renderizan primero
    * Valor por defecto: `10`
* `acs_type`: (`string`) tipo de este ACS
    * _opcional_
    * Se usa con `mux_type` para determinar automáticamente qué ACS quitar al intentar ponerse este ACS.
    * En general, esto debería usarse si prevés múltiples versiones de un ACS similar (lazos, tazas).
    * Si necesitas algo parecido a "etiquetas", usa `ex_props` en su lugar.
    * También se usa con el sistema `ACSTemplate` para aplicar valores por defecto a ciertas propiedades. Consulta [ACSTemplates](#acstemplates) para más información.
    * Valor por defecto: `None`
* `mux_type`: (`list of strings`) lista de tipos de ACS con los que este ACS entra en conflicto
    * _opcional_
    * Se usa con `acs_type` para determinar automáticamente qué ACS quitar al intentar ponerse este ACS.
    * Los ACS con tipos incluidos aquí se **eliminarán** al intentar ponerse este ACS.
    * Valor por defecto: `None`
* `giftname`: (`string`) nombre de archivo del regalo asociado al sprite
    * _opcional_
    * Proporcionar `giftname` permite regalarle este sprite a Monika.
    * **No** incluyas la extensión del archivo.
    * **No** incluyas la ruta del archivo.
    * **Si no se proporciona, el sprite no se podrá desbloquear mediante regalos y, por tanto, no será desbloqueable con el sistema estándar.** Los sprites aún pueden desbloquearse por programación.
    * Valor por defecto: `None`
* `arm_split`: (`object`) [Objeto PoseMap](#posemap-object)
    * **obligatorio** si `rec_layer` es 8 (BSE) o 9 (ASE). En otros casos se ignora
    * cada valor debe ser una cadena (`string`). Consulta [Objeto `PoseMap`](#posemap-object) para obtener más información.
    * si se omite, se creará un ACS normal
* `dlg_desc`: (`string`) nombre amigable del accesorio para usar en diálogos
    * _opcional_
    * Se usa en los diálogos al referirse al accesorio.
    * Debe estar en minúsculas.
    * Debe proporcionarse junto con `dlg_plural`
* `dlg_plural`: (`boolean`) determina si `dlg_desc` debe usarse con adjetivos/adverbios en plural o singular
    * _opcional_
    * Se usa en los diálogos al referirse al accesorio.
    * Debe proporcionarse junto con `dlg_desc`
* `keep_on_desk`: (`boolean`) determina si este ACS debe quedarse en el escritorio cuando Monika no está en el escritorio
    * _opcional_
    * Valor por defecto: `false`

### Específico de `Hair`
Estas propiedades son solo para sprites `Hair`.

* `unlock`: (`boolean`) determina si este sprite debe desbloquearse automáticamente o no
    * _opcional_
    * `True` significa que el sprite de peinado se desbloquea automáticamente. `False` significa que no se desbloquea automáticamente.
    * **Si es `False`, el sprite solo puede desbloquearse por programación.**
    * Valor por defecto: `true`
* `mid_hair_map`: (`object`) [Objeto `PoseMap`](#posemap-object)
    * _opcional_
    * Permite capas de pelo entre el cuerpo y la cabeza (`mid`). Consulta [#7148](https://github.com/Monika-After-Story/MonikaModDev/pull/7148).
    * Valor por defecto: `None`

### Específico de `Clothes`
Estas propiedades son solo para sprites `Clothes`.

* `hair_map`: (`object`) diccionario que mapea peinados a otros peinados
    * _opcional_
    * Permite reemplazar peinados por otros peinados al llevar esta ropa.
    * **Las claves deben ser cadenas (`string`).** Deben ser IDs de sprites `Hair` (excepto `all`).
    * **Los valores deben ser cadenas (`string`).** Deben ser IDs de sprites `Hair`.
    * Usar la clave `all` establecerá una sustitución de peinado predeterminada. Si no se establece explícitamente, se usará `def` (el peinado de coleta por defecto)
    * **NOTA:** El modo dryrun **no** detectará claves/valores que **no existan**. En su lugar, se registran advertencias y se modifican propiedades para evitar fallos.
* `giftname`: (`string`) igual que `giftname` en [sprites ACS](#acs-specific)
    * Igual que `giftname` en [sprites ACS](#acs-specific)
* `pose_arms`: (`object`) [Objeto `PoseArms`](#posearms-object)
    * _opcional_
    * Si no se proporciona, se usan los `pose_arms` definidos internamente que siguen los sprites base.
* `outfit_hair`: (`string`) peinado que combina con esta ropa para un conjunto
    * _opcional_
    * Debe ser el ID de un sprite `Hair`.
* `outfit_acs`: (`list of strings`) lista de ACS que combinan con esta ropa para un conjunto
    * _opcional_
    * Cada string debe ser el ID de un ACS.

<a id="posemap-object"></a>
### Objeto `PoseMap`
Estas propiedades son para objetos `PoseMap`.

* `mpm_type`: (`int`) tipo de este mapa de poses
    * **obligatorio** para `pose_map` en `Hair` y `Clothes`
    * _opcional_ para otras propiedades
    * Para `pose_map` en `Hair` y `Clothes`, debe establecerse en uno de los siguientes valores:
        * 0 - si `pose_map` debe tratarse en modo activar/desactivar
        * 1 - si `pose_map` debe tratarse en modo de reserva (`fallback`)
    * Para ACS y todas las demás propiedades, esto se sobrescribirá internamente con el tipo correcto.
    * Valor por defecto: definido internamente
* `default`: (`boolean | string | object`) valor que se usará por defecto para todas las poses no inclinadas
    * _opcional_
    * Valor por defecto: `None`
* `l_default`: (`boolean | string | object`) valor que se usará por defecto para todas las poses inclinadas
    * _opcional_
    * Valor por defecto: `None`
* `use_reg_for_l`: (`boolean`) determina si los valores por defecto de poses inclinadas deben usar los valores por defecto normales
    * _opcional_
    * `True` usará `default` en lugar de `l_default` en las situaciones correspondientes. `False` tratará ambos valores por separado.
    * Valor por defecto: `False`
* `p1`: (`boolean | string | object`) valor a usar para la pose 1
    * _opcional_
    * Es la pose "steepling".
    * Valor por defecto: `None`
* `p2`: (`boolean | string | object`) valor a usar para la pose 2
    * _opcional_
    * Es la pose "crossed".
    * Valor por defecto: `None`
* `p3`: (`boolean | string | object`) valor a usar para la pose 3
    * _opcional_
    * Es la pose "restleftpointright".
    * Valor por defecto: `None`
* `p4`: (`boolean | string | object`) valor a usar para la pose 4
    * _opcional_
    * Es la pose "pointright".
    * Valor por defecto: `None`
* `p5`: (`boolean | string | object`) valor a usar para la pose 5
    * _opcional_
    * Es la pose "lean|def".
    * Valor por defecto: `None`
* `p6`: (`boolean | string | object`) valor a usar para la pose 6
    * _opcional_
    * Es la pose "down".
    * Valor por defecto: `None`
* `p7`: (`boolean | string | object`) valor a usar para la pose 7
    * _opcional_
    * Es la pose "downleftpointright"
    * Valor por defecto: `None`

Muchos de los valores (excepto `use_reg_for_l`) cambian según el tipo de sprite:

* ACS:
    * `pose_map` - cada valor debe ser una cadena (`string`) que indique el código de imagen que se va a usar. Por ejemplo, si se establece en "0", se asume que el ACS tiene una imagen como `acs-mug-0.png`
    * `arm_split` - solo se usa si el `rec_layer` del ACS es ASE o BSE. Cada valor debe ser una cadena (`string`) delimitada por carets (`^`) como `5^10`. Códigos de capa disponibles:
        * "0" - este ACS tiene una capa body-0 o arms-0 (`acs-mug-0-0.png`) para esta pose
        * "1" - este ACS tiene una capa body-1 (`acs-mug-0-1.png`) para esta pose
        * "5" - este ACS tiene una capa arms-5 (`acs-mug-0-5.png`) para esta pose
        * "10" - este ACS tiene una capa arms-10 (`acs-mug-0-10.png`) para esta pose
        * "" - este ACS no tiene capas para esta pose (no se renderiza)
        * "*" - este ACS tiene todas las capas para esta pose
* `Hair`:
    * `pose_map` - cada valor debe ser un booleano o una cadena (`string`), según `mpm_type`
        * si `mpm_type` es 0, cada valor debe ser un booleano. `True` indica que la pose debe estar habilitada; `False`, que debe estar deshabilitada.
        * si `mpm_type` es 1, cada valor debe ser una pose en formato `string` (ver abajo). Esa pose se usa en lugar de la pose real.
    * `mid_hair_map` - cada valor debe ser un booleano. `True` indica que la pose tiene una capa de pelo `mid`; `False`, que no la tiene.
* `Clothes`:
    * `pose_map` - mismas reglas que `Hair`.

**Poses disponibles:**

* `steepling` - pose original de DDLC
* `crossed` - brazos cruzados
* `restleftpointright` - steepling, excepto que la mano derecha apunta a la derecha
* `pointright` - el brazo izquierdo está abajo y el derecho se extiende mucho hacia la derecha y señala a la derecha
* `down` - ambos brazos abajo
* `downleftpointright` - el brazo izquierdo está abajo y el derecho está en reposo apuntando a la derecha
* `def|def` - inclinación por defecto con brazos por defecto

<a id="selectable-object"></a>
### Objeto `Selectable`
Estas propiedades son para objetos `Selectable` (`select_info`).

* `display_name`: (`string`) nombre amigable de este sprite
    * **obligatorio**
    * Esto se muestra al usuario en los menús de selección.
* `thumb`: (`string`) nombre de archivo de la miniatura de este sprite
    * **obligatorio**
    * Esto se muestra al usuario como miniatura en los menús de selección.
* `group`: (`string`) ID del grupo al que debe asociarse este elemento seleccionable
    * **obligatorio**
    * Se usa para agrupar elementos seleccionables, de modo que los sprites relacionados puedan elegirse en el menú de selección adecuado.
* `visible_when_locked`: (`boolean`) determina si el sprite debe verse en el menú de selección incluso estando bloqueado
    * _opcional_
    * `True` permitirá que el sprite aparezca en el menú de selección cuando esté bloqueado. `False` hará que solo aparezca cuando esté desbloqueado.
    * Valor por defecto: `True`
* `select_dlg`: (`list of strings`) lista de líneas que Monika debe decir cuando este sprite ha sido seleccionado
    * _opcional_
    * Cada string se trata como un mensaje independiente, elegido de forma aleatoria.
    * Hay soporte para sustituciones (es decir, usando corchetes), pero se limita a variables globales.
    * La expresión **no** se puede ajustar por línea. En general, se usa `1eua`.
    * Cuando el sprite ha sido "seleccionado", Monika pasa a llevar ese sprite.
    * Valor por defecto: `None`

<a id="posearms-object"></a>
### Objeto `PoseArms`
Este es un mapeo de todos los brazos disponibles.
Si se omite algún brazo, significa que no se debe mostrar ninguna capa para ese brazo.
Un objeto vacío significa que esta ropa no tiene capas de brazo.

* `crossed`: (`object`) [Objeto `PoseArm`](#posearm-object)
    * _opcional_
    * datos de pose de brazo para brazos cruzados
* `left-down`: (`object`) [Objeto `PoseArm`](#posearm-object)
    * _opcional_
    * datos de pose de brazo para el brazo izquierdo abajo
* `left-rest`: (`object`) [Objeto `PoseArm`](#posearm-object)
    * _opcional_
    * datos de pose de brazo para el brazo izquierdo en reposo
* `right-down`: (`object`) [Objeto `PoseArm`](#posearm-object)
    * _opcional_
    * datos de pose de brazo para el brazo derecho abajo
* `right-point`: (`object`) [Objeto `PoseArm`](#posearm-object)
    * _opcional_
    * datos de pose de brazo para el brazo derecho señalando
* `right-restpoint`: (`object`) [Objeto `PoseArm`](#posearm-object)
    * _opcional_
    * datos de pose de brazo para el brazo derecho en reposo señalando
* `steepling`: (`object`) [Objeto `PoseArm`](#posearm-object)
    * _opcional_
    * datos de pose de brazo para brazos steepling
* `def|left-def`: (`object`) [Objeto `PoseArm`](#posearm-object)
    * _opcional_
    * datos de pose de brazo para el brazo inclinado-def-left-def
* `def|right-def`: (`object`) [Objeto `PoseArm`](#posearm-object)
    * _opcional_
    * datos de pose de brazo para el brazo inclinado-def-right-def

<a id="posearm-object"></a>
### Objeto `PoseArm`
Representación de un único brazo.

* `tag`: (`string`) nombre de la cadena de brazo que se usará al renderizar este brazo
    * **obligatorio**
    * se usa en formatos como `arms-<tag>` o `arms-left/right-<tag>`
* `layers`: (`string`) cadena delimitada por carets (^) que indica capas para este brazo
    * **obligatorio**
    * valores aceptables:
        * "*" - este brazo existe en todas las capas
        * "0" - este brazo existe en la capa 0
        * "5" - este brazo existe en la capa 5
        * "10" - este brazo existe en la capa 10
        * "" - este brazo no existe en ninguna capa
    * la cadena delimitada debería verse así: `5^10`
* `highlight`: (`object`) [Objeto `Highlight`](#highlight-object)
    * _opcional_
    * resaltados que se usarán para este brazo

<a id="highlightsplit-object"></a>
### Objeto `HighlightSplit`
Los objetos `HighlightSplit` son solo para `Split ACS`. Las claves deben ser las mismas que los valores usados en `pose_map`. Los valores deben ser [objetos `Highlight`](#highlight-object), donde las claves sean las listadas más abajo para `HighlightSplit`. Estas también deben ser las mismas que se usen para `arm_split`.

Aquí tienes un ejemplo abreviado:
```json
{
    "pose_map": {
        "p1": "1",
        "p2": "2",
        "p7": "7"
    },
    "arm_split": {
        "p1": "10",
        "p2": "5^10",
        "p7": "0"
    },
    "highlight": {
        "1": {
            "mapping": {
                "10": {
                    "night": "0"
                }
            }
        },
        "2": {
            "mapping": {
                "5": {
                    "night": "1"
                },
                "10": {
                    "night": "2"
                }
            }
        },
        "7": {
            "mapping": {
                "0": {
                    "night": "3"
                }
            }
        }
    }
}
```

<a id="highlight-object"></a>
### Objeto `Highlight`

* `default`: (`object`) [Objeto `Filter`](#filter-object)
    * _opcional_
    * resaltados predeterminados que se aplicarán
    * esto debería usarse rara vez
* `mapping`: (`object`) objeto basado en diccionario
    * _opcional_
    * Las claves variarán según el objeto contenedor.
    * Los valores deben ser [objetos `Filter`](#filter-object)

Las claves de los objetos `Highlight` variarán según el objeto que contenga la propiedad `highlight`.
Todas las claves son cadenas (`string`).

* ACS
    * las claves deben ser las mismas que los valores usados en la propiedad `pose_map`
* `Hair`
    * `front` - resaltados que se aplican a la capa frontal de un objeto `Hair`
    * `back` - resaltados que se aplican a la capa trasera de un objeto `Hair`
    * `mid` - resaltados que se aplican a la capa media de un objeto `Hair`
    * `def|front` - resaltados que se aplican a la capa frontal inclinada de un objeto `Hair`
    * `def|back` - resaltados que se aplican a la capa trasera inclinada de un objeto `Hair`
    * `def|mid` - resaltados que se aplican a la capa media inclinada de un objeto `Hair`
* `Clothes`
    * `0` - resaltados que se aplican a la capa body-0 de un objeto `Clothes`
    * `1` - resaltados que se aplican a la capa body-1 de un objeto `Clothes`
    * `def|0` - resaltados que se aplican a la capa body-0 inclinada de un objeto `Clothes`
    * `def|1` - resaltados que se aplican a la capa body-1 inclinada de un objeto `Clothes`
* Objeto `PoseArm`
    * `0` - resaltados que se aplican a la capa arm-0 de un objeto de brazo
    * `5` - resaltados que se aplican a la capa arm-5 de un objeto de brazo
    * `10` - resaltados que se aplican a la capa arm-10 de un objeto de brazo
* Objeto `HighlightSplit`
    * `0` - resaltados que se aplican a la capa acs-0
    * `1` - resaltados que se aplican a la capa acs-1
    * `5` - resaltados que se aplican a la capa acs-5
    * `10` - resaltados que se aplican a la capa acs-10

<a id="filter-object"></a>
### Objeto `Filter`
Los objetos `Filter` asignan filtros específicos a códigos de resaltado, que determinan qué capa de resaltado usar según el filtro actual. Estos códigos de resaltado se añaden al final de los archivos (antes de la extensión) como `-h#`, donde `#` es el código.

* `default`: (`string`) código de resaltado por defecto que se usará
    * _opcional_
    * se aplica siempre, independientemente del filtro
    * esto debería usarse rara vez
* `day`: (`string`) código de resaltado que se usará para el filtro de día
    * _opcional_
    * se aplica cuando se usa el filtro de día
* `night`: (`string`) código de resaltado que se usará para el filtro de noche
    * _opcional_
    * se aplica cuando se usa el filtro de noche

<a id="file-locations"></a>
<a id="ubicaciones-de-archivos"></a>
# Ubicaciones de archivos

Todos los JSON de sprites deben añadirse en `game/mod_assets/monika/j/`. Cuando se inicia MAS, el archivo `log/spj.log` contendrá mensajes sobre los sprites, incluidas advertencias y errores encontrados durante el análisis. Los errores significan que el sprite **no** se cargó. Las advertencias significan que el sprite se cargó, pero puede dar problemas más adelante.

Los archivos de arte deben ir en las carpetas correspondientes, pero la estructura exacta depende de la `version`.

Independientemente de la versión, el archivo de registro `spj.log` mostrará advertencias si los sprites correspondientes no se encuentran o no se pueden cargar.

Para toda la ropa y miniaturas:

* `game/mod_assets/monika/c/clothing_name/*` - ropa
* `game/mod_assets/thumbs/*` - miniaturas para selectores

<a id="version-4-file-locations-v01216"></a>
### Ubicaciones de archivos de la versión 4 (v0.12.16+)

ACS y `Hair` deben tener su propia subcarpeta dentro de `a/` y `h/`, correspondiente a su campo `img_sit`:

* `game/mod_assets/monika/a/acs_name/*` - ACS
* `game/mod_assets/monika/h/hair_name/*` - `Hair`

Los nombres de archivo **no** deben incluir la cadena del campo `img_sit`. Por ejemplo, con un JSON como este:
```json
{
    "version": 4,
    "type": 0,
    "img_sit": "filenameacs",
    "pose_map": {
        "p1": "0",
        "p2": "1",
        "p5": "5"
    }
}
```

Los archivos y rutas deberían verse así:

* `a/filenameacs/0.png`
* `a/filenameacs/1.png`
* `a/filenameacs/5.png`

<a id="version-3-file-locations-v0110-v01215"></a>
### Ubicaciones de archivos de la versión 3 (v0.11.0 - v0.12.15)

ACS y `Hair` deben colocarse directamente en las carpetas `a/` y `h/`:

* `game/mod_assets/monika/a/*` - ACS
* `game/mod_assets/monika/h/*` - `Hair`

Los nombres de archivo deben incluir la cadena del campo `img_sit`. Por ejemplo, con un JSON como este:
```json
{
    "version": 3,
    "type": 0,
    "img_sit": "filenameacs",
    "pose_map": {
        "p1": "0",
        "p2": "1",
        "p5": "5"
    }
}
```

Los archivos y rutas deberían verse así:
* `a/acs-filenameacs-0.png`
* `a/acs-filenameacs-1.png`
* `a/acs-filenameacs-5.png`

<a id="prog-points"></a>
<a id="puntos-prog"></a>
# Puntos prog

A los sprites JSON se les pueden seguir asignando puntos prog, aunque estos se determinan por programación. Los puntos prog deben existir en el nivel de init -2 del store `mas_sprites` con el siguiente formato de nombre:

* ACS:
    * `_acs_name_entry`
    * `_acs_name_exit`
* HAIR:
    * `_hair_name_entry`
    * `_hair_name_exit`
* CLOTHES:
    * `_clothes_name_entry`
    * `_clothes_name_exit`

`Name` en los formatos anteriores se sustituye por la propiedad `name` del JSON.

En el arranque se comprueba que los puntos prog existan y sean invocables, y se registran en `log/spj.log` independientemente del estado de `dryrun`. Los puntos prog también se pueden comprobar usando un tema de desarrollo ubicado en `dev/dev_sprites`. Esta herramienta se recomienda para probar puntos prog, ya que captura excepciones y evita cierres inesperados.

<a id="gift-reactions"></a>
<a id="reacciones-de-regalos"></a>
# Reacciones de regalos

Si se rellena `giftname`, el sprite se añade al sistema de reacciones. Este intenta usar etiquetas explícitas antes de recurrir a etiquetas genéricas. Las etiquetas de reacción deben tener los siguientes nombres:

* ACS : `mas_reaction_gift_acs_<name>`
* HAIR: `mas_reaction_gift_hair_<name>`
* CLOTHES: `mas_reaction_gift_clothes_<name>`

donde `<name>` se sustituye por la propiedad `name` del JSON.

La etiqueta de reacción genérica es `mas_reaction_gift_generic_sprite_json`.

Todas las etiquetas de reacción **deben** empezar con una llamada a `mas_getSpriteObjInfo` y terminar con una llamada a `mas_finishSpriteObjInfo` antes de la llamada a la función de borrado de archivos. Consulta la etiqueta de reacción genérica para ver un ejemplo. Consulta también las funciones correspondientes en `zz_reactions` para más información.

<a id="available-exprops"></a>
<a id="exprops-disponibles"></a>
# Exprops disponibles

| exprop                    | ACS?  | peinado?  | ropa?     | efectos   | valor |
| ---                       | :---: | :---:     | :---:     | ---       | ---   |
| `bare-right-shoulder`     |       |           | X         | indica que esta ropa deja el hombro derecho al descubierto | ignorado |
| `cosplay`                 |       |           | X         | indica que esta ropa es de cosplay | ignorado |
| `costume`                 |       |           | X         | indica que esta ropa es un disfraz | ignorado |
| `desired-ribbon`          |       |           | X         | fuerza a llevar un lazo al cambiar a esta ropa | el `name` del lazo que se debe llevar, como `string` |
| `drink`                   | X     |           |           | indica que este ACS es un objeto de bebida | ignorado |
| `excluded-clothes-props`  |       | X         |           | limita este peinado para que solo pueda llevarse con ropa que **no** contenga ninguno de los `ex_props` especificados | lista de `ex_props` que se excluirán, como lista de `string` |
| `excluded-hair-props`     | X     |           |           | limita este ACS para que solo pueda llevarse con peinados que **no** contengan ninguno de los `ex_props` especificados | lista de `ex_props` que se excluirán, como lista de `string` |
| `food`                    | X     |           |           | indica que este ACS es un objeto de comida | ignorado |
| `left-desk-acs`           | X     |           |           | indica que este ACS está en el lado izquierdo del escritorio de Monika. Se usa para evitar superponer ACS en el mismo sitio | ignorado |
| `lingerie`                |       |           | X         | indica que esta ropa es lencería | ignorado |
| `no-tails`                |       | X         |           | indica que este peinado no tiene coletas | ignorado |
| `required-clothes-prop`   |       | X         |           | limita este peinado para que solo pueda llevarse con ropa que contenga un `ex_prop` específico | el `ex_prop` que este peinado requiere, como `string` |
| `required-hair-prop`      | X     |           |           | limita este ACS para que solo pueda llevarse con peinados que contengan un `ex_prop` específico | el `ex_prop` que este ACS requiere, como `string` |
| `ribbon`                  |       | X         |           | habilita lazos para este peinado | ignorado |
| `ribbon-like`             | X     |           |           | indica que este ACS debe considerarse similar a un lazo, pero no es una versión directa del lazo principal | ignorado |
| `ribbon-off`              |       | X         |           | quita el lazo si se lleva puesto al cambiar a este peinado | ignorado |
| `ribbon-restore`          |       | X         |           | restaura el lazo usado previamente al cambiar a este peinado, si se encuentra | ignorado |
| `tiedstrand`              |       | X         |           | indica que este peinado es de tipo `tiedstrand` | ignorado |
| `twin-ribbon`             | X     |           |           | indica que este ACS es un ACS basado en `twin-ribbon` | ignorado |
| `twintails`               |       | X         |           | indica que este peinado es de tipo `twintail` | ignorado |

<a id="acstemplates"></a>
# ACSTemplates

`ACSTemplates` se usa para asignar valores por defecto a ciertas propiedades. Se pueden seguir proporcionando propiedades personalizadas mediante JSON, pero **no** sobrescribirán los valores por defecto que aportan las plantillas.
**NOTA:** Es posible que `ACSTemplates` no esté completamente actualizado a partir de la versión 0.11.0. Separaré esto (y las exprops) en una página independiente que se generará automáticamente.

Propiedades que se pueden plantillar:

* `mux_type`
* `ex_props`
* `keep_on_desk`

Aquí tienes la lista de plantillas actuales y qué valores por defecto aplican.
Los elementos en MAYÚSCULAS se describen en la segunda tabla.

| `acs-type`                | `mux_type` por defecto | `ex_props` por defecto |
| ---                       | ---                   | ---                   |
| `bow`                     | `DEF_MUX_RB`          | `ribbon-like: True`, `excluded-hair-props: DEF_EXP_TT_EXCL` |
| `bunny-scrunchie`         | `DEF_MUX_RB`          | `ribbon-like: True`, `excluded-hair-props: DEF_EXP_TT_EXCL` |
| `headband`                | `DEF_MUX_HB`          |                       |
| `headset`                 | `DEF_MUX_HS`          |                       |
| `left-hair-clip`          | `DEF_MUX_LHC`         | `left-hair-strand-eye-level: True` |
| `left-hair-flower`        | `left-hair-flower`, `left-hair-flower-ear` | `left-hair-strand-eye-level: True` |
| `left-hair-flower-ear`    | `DEF_MUX_LHFE`        | `left-hair-strand-eye-level: True` |
| `mug`                     | `mug`                 |                       |
| `necklace`                | `necklace`            | `bare collar: True`   |
| `ribbon`                  | `DEF_MUX_RB`          |                       |
| `twin-ribbons`            | `DEF_MUX_RB`          | `twin-ribbon: True`, `ribbon-like: True`, `required-hair-prop: twintails` |
| `wrist-bracelet`          | `wrist-bracelet`      | `bare wrist: True`    |

| `elemento`        | `valor`   |
| ---               | ---       |
| `DEF_EXP_TT_EXCL` | `twintails` |
| `DEF_MUX_RB`      | `ribbon`, `bow`, `bunny-scrunchie`, `hat`, `s-type-ribbon`, `twin-ribbons` |
| `DEF_MUX_HAT`     | `hat`, `bow`, `bunny-scrunchie`, `earphones`, `front-hair-flower-crown`, `headband`, `headphones`, `headset`, `left-hair-flower`, `ribbon`, `s-type-ribbon`, `twin-tibbons` |
| `DEF_MUX_HB`      | `headband`, `hat`, `headphones`, `headset` |
| `DEF_MUX_HS`      | `headset`, `earphones`, `hat`, `headband`, `headphones`, `left-hair-flower-ear` |
| `DEF_MUX_LD`      | `chocs`, `plate`, `plush_q` |
| `DEF_MUX_LHC`     | `left-hair-clip` |
| `DEF_MUX_LHFE`    | `left-hair-flower-ear`, `earphones`, `front-hair-flower-crown`, `hat`, `headset`, `headphones`, `left-hair-flower` |

<a id="version-history"></a>
<a id="historial-de-versiones"></a>
# Historial de versiones

* 0.12.16 - versiones actualizadas y se añadió información sobre la nueva estructura de archivos
* 0.11.0 - se añadió la propiedad `keep_on_desk` a `ACSTemplates`. Se eliminó `hover_dlg` de los JSON. Se añadió `highlight` a los JSON. Se actualizó `pose_arms` para los JSON. Se añadieron las exprops `bare-right-shoulder`, `drink`, `excluded-clothes-props`, `food`, `left-desk-acs`, `lingerie`, `no-tails`, `required-clothes-prop`, `tiedstrand`
* 0.10.4 - se actualizaron `left-hair-flower` y `bow` en `ACSTemplates`, y se añadió `bunny-scrunchie`. Se añadió la exprop `excluded-hair-props`.
* 0.10.3 - se actualizó `left-hair-flower` en `ACSTemplates` y se añadió `left-hair-flower-ear`
* 0.10.2 - se añadieron las exprops `ribbon-like`, `required-hair-prop`, `twintails`, `costume` y `cosplay`. Se añadieron `dlg_desc` y `dlg_plural`. Se añadieron `ACSTemplates`.
* 0.10.0 - actualizado para funcionar con el nuevo sistema `split-base`
* 0.9.4 - creado
