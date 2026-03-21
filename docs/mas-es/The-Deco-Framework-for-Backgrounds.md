La versión 0.11.7 introdujo el framework de decoración basado en image tags (etiquetas de imagen), que permite ocultar/mostrar automáticamente una image tag en distintas ubicaciones según el fondo actual.

La versión 0.12.3 introdujo el reemplazo de image tags, que permite usar una image tag completamente distinta en diferentes fondos.

Esta guía está escrita para **creadores de fondos personalizados** y no profundiza en los aspectos técnicos del framework.
Consulta [Uso](./The-Deco-Framework-for-Backgrounds.md#usage) para saltarte las explicaciones sobre el fondo.

# Índice
* [Componentes](./The-Deco-Framework-for-Backgrounds.md#components)
    * [`MASImageTagDecoration`](./The-Deco-Framework-for-Backgrounds.md#masimagetagdecoration)
    * [`MASAdvancedDecoFrame`](./The-Deco-Framework-for-Backgrounds.md#masadvanceddecoframe)
    * [`MASImageTagDecoDefinition`](./The-Deco-Framework-for-Backgrounds.md#masimagetagdecodefinition)
* [Comportamiento del sistema](./The-Deco-Framework-for-Backgrounds.md#system-behavior-simplified)
* [Uso](./The-Deco-Framework-for-Backgrounds.md#usage)
    * [Paso 1 - determina qué objetos de decoración te sirven](./The-Deco-Framework-for-Backgrounds.md#step-1-determine-which-decoration-objects-work-for-your-background)
    * [Paso 2 - registra esos objetos para tu fondo](./The-Deco-Framework-for-Backgrounds.md#step-2-register-those-decoration-objects-for-your-background)
* [Objetos de decoración estándar](./The-Deco-Framework-for-Backgrounds.md#standard-decoration-objects)
    * [player-bday](./The-Deco-Framework-for-Backgrounds.md#player-bday)
    * [o31](./The-Deco-Framework-for-Backgrounds.md#o31)
    * [d25](./The-Deco-Framework-for-Backgrounds.md#d25)
* [APIs](./The-Deco-Framework-for-Backgrounds.md#apis)
    * [`MASImageTagDecoDefinition.register_img`](./The-Deco-Framework-for-Backgrounds.md#masimagetagdecodefinitionregister_img)
    * [`MASImageTagDecoDefinition.register_img_same`](./The-Deco-Framework-for-Backgrounds.md#masimagetagdecodefinitionregister_img_same)
    * [`mas_showDecoTag`](./The-Deco-Framework-for-Backgrounds.md#mas_showdecotag)
    * [`mas_hideDecoTag`](./The-Deco-Framework-for-Backgrounds.md#mas_hidedecotag)
    * [`mas_isDecoTagEnabled`](./The-Deco-Framework-for-Backgrounds.md#mas_isdecotagenabled)
    * [`mas_isDecoTagVisible`](./The-Deco-Framework-for-Backgrounds.md#mas_isdecotagvisible)

<a id="components"></a>
# Componentes

<a id="masimagetagdecoration"></a>
### `MASImageTagDecoration`

Esta es una representación en objeto de una decoración que corresponde a una image tag.
Su objetivo principal es permitir asociar datos adicionales a una decoración, como `ex_props`, por ejemplo.

En general, **no** tendrás que construir estos objetos.

<a id="masadvanceddecoframe"></a>
### `MASAdvancedDecoFrame`

Almacena atributos que se pasarían a `renpy.show`. Es parecido al currying (una forma de preparar funciones con parámetros fijados).
Esto **solo** debe usarse con objetos `MASImageTagDecoration`

Probablemente tendrás que construir estos objetos para definir la posición de una decoración.
El constructor recibe los mismos parámetros que [renpy.show](https://www.renpy.org/doc/html/statement_equivalents.html#renpy.show), **excluyendo name.**

<a id="masimagetagdecodefinition"></a>
### `MASImageTagDecoDefinition`

Vincula image tags (objetos `MASImageTagDecoration`) con objetos `MASAdvancedDecoFrame` para fondos concretos.
Toda decoración basada en image tags debe tener uno de estos para que el framework deco considere esa tag como una decoración.

En general, **no** tendrás que construir estos objetos.

<a id="system-behavior-simplified"></a>
# Comportamiento del sistema (simplificado)

Cuando queremos mostrar una decoración, le pedimos al sistema que la muestre mediante la función show tag. Eso prepara la decoración para mostrarse si tiene una entrada en su `MASImageTagDecoDefinition` para el fondo actual. Sin embargo, la imagen real solo se muestra cuando cambia el fondo o hay un cambio de escena, lo que permite que la imagen se disuelva en la escena de forma limpia.

El sistema gestiona automáticamente tanto la ocultación como la visualización de decoraciones según los objetos `MASImageTagDecoDefinition`. Si una decoración no tiene un mapeo (asignación entre elementos) a un objeto `MASAdvancedDecoFrame` en su `MASImageTagDecoDefinition`, la decoración se oculta. En caso contrario, los objetos `MASAdvancedDecoFrame` permiten mostrar decoraciones en distintas ubicaciones según el fondo.

<a id="usage"></a>
# Uso

<a id="step-1-determine-which-decoration-objects-work-for-your-background"></a>
### Paso 1 - determina qué objetos de decoración te sirven para tu fondo

Tendrás que revisar cada imagen de decoración y decidir si puede mostrarse en tu fondo. Si puede, tendrás que especificar un objeto `MASAdvancedDecoFrame` (o usar uno existente) para definir la mejor posición en ese fondo.

Si debe mostrarse una imagen diferente, puedes asociar otra image tag (y, opcionalmente, un frame) con la decoración para tu fondo.

Para ver la lista de objetos de decoración actuales, consulta [aquí (enlace)](./The-Deco-Framework-for-Backgrounds.md#standard-decoration-objects)

<a id="step-2-register-those-decoration-objects-for-your-background"></a>
### Paso 2 - registra esos objetos de decoración para tu fondo

Tendrás que escribir una línea por cada objeto de decoración que quieras permitir en tu fondo. Esto debe colocarse *después* del código que crea el objeto de fondo.

Aquí puedes usar 2 APIs (interfaces de funciones del sistema):

<a id="masimagetagdecodefinitionregister_img"></a>
#### `MASImageTagDecoDefinition.register_img`
Parámetros:

* `tag` - (**REQUIRED**) image tag del objeto de decoración con el que registrar
* `bg_id` - (**REQUIRED**) ID del objeto de fondo que se va a registrar (debe ser el ID de **tu** fondo)
* `adv_deco_frame` - (**REQUIRED**) objeto `MASAdvancedDecoFrame` que se usará al mostrar esta decoración en tu fondo
* `replace_tag` - (*optional*) - **NEW in 0.12.3+** - image tag que se usará en lugar de la imagen de decoración estándar

Usa esta función cuando el objeto de decoración se pueda mostrar en tu fondo, pero en una ubicación distinta a la predeterminada.

Aquí tienes un ejemplo que registra el árbol de Navidad en tu fondo usando un zorder de 7. (El valor por defecto es 6)
```python
MASImageTagDecoDefinition.register_img(
    "mas_d25_tree",
    "your_custom_background_id",
    MASAdvancedDecoFrame(zorder=7)
)
```

Aquí tienes un ejemplo que registra un árbol personalizado en tu fondo.
```python
MASImageTagDecoDefinition.register_img(
    "mas_d25_tree",
    "your_custom_background_id",
    MASAdvancedDecoFrame(),
    replace_tag="your_custom_d25_tree"
)
```

<a id="masimagetagdecodefinitionregister_img_same"></a>
#### `MASImageTagDecoDefinition.register_img_same`
Parámetros:

* `tag` - (**REQUIRED**) image tag del objeto de decoración con el que registrar
* `bg_id_src` - (**REQUIRED**) ID del objeto de fondo del que copiar `MASAdvancedDecoFrame`
* `bg_id_dest` - (**REQUIRED**) ID del objeto de fondo que se va a registrar (debe ser el ID de **tu** fondo)

Usa esta función si el objeto de decoración puede mostrarse en tu fondo en la misma posición en la que se muestra en otro fondo. Por ejemplo, si la ubicación predeterminada de una decoración ya te sirve, aquí pasarías `store.mas_background.MBG_DEF`.

Aquí tienes un ejemplo que registra el árbol de Navidad en tu fondo usando la posición predeterminada.
```python
MASImageTagDecoDefinition.register_img_same(
    "mas_d25_tree",
    store.mas_background.MBG_DEF,
    "your_custom_background_id"
)
```

### Paso 3 - completado

¡Y ya está! Una vez registres las imágenes, el framework Deco debería encargarse del resto.


<a id="standard-decoration-objects"></a>
# Objetos de decoración estándar

Para probar cómo se ven y su posición predeterminada, usa la API show deco con `show_now` en True.
**NOTA:** probablemente todas las imágenes compuestas no funcionen en otros fondos. Lo sentimos.

<a id="player-bday"></a>
### player-bday
* **próximamente**

<a id="o31"></a>
### o31
* `mas_o31_wall_candle` - vela enjaulada sostenida por una mano demonik(a)
* `mas_o31_cat_frame` - un cuadro de gato en la pared detrás de Monika que es algo más de lo que parece
* `mas_o31_wall_bats` - adhesivos de murciélagos para la pared bajo el calendario
* `mas_o31_window_ghost` - fantasma de papel que cuelga de la ventana
* `mas_o31_cobwebs` - telarañas + araña que cuelgan por las esquinas de la habitación
* `mas_o31_candles` - mesa con un candelabro de 2 brazos
* `mas_o31_jack_o_lantern` - jack o' lantern colocada en la parte trasera izquierda de la habitación
* `mas_o31_garlands` - una tira de banderines de o31 que, supongo, llamamos guirnaldas
* `mas_o31_ceiling_lights` - bombillas que cuelgan del techo
* `mas_o31_ceiling_deco` - decoración que cuelga del techo
* `mas_o31_vignette` - viñeta especial específica de o31

<a id="d25"></a>
### d25
* `mas_d25_banners` - composición de corona y calcetín.
* `mas_d25_garlands` - cosa verde que supongo que se llama guirnaldas
* `mas_d25_gifts` - regalos que van debajo del árbol de Navidad
* `mas_d25_lights` - luces que van alrededor de la habitación
* `mas_d25_tree` - árbol de Navidad

<a id="apis"></a>
# APIs

<a id="mas_showdecotag"></a>
### `mas_showDecoTag`
Parámetros:

* `tag` - (**REQUIRED**) image tag de la decoración que se va a mostrar
* `show_now` - [*optional*] pasa True para mostrar una decoración de inmediato; con False se esperará al siguiente cambio de fondo o de escena.

Esta es la forma principal de mostrar una decoración. `show_now` solo se recomienda en pruebas, ya que no disolverá las imágenes dentro de la escena.

<a id="mas_hidedecotag"></a>
### `mas_hideDecoTag`
Parámetros:

* `tag` - (**REQUIRED**) image tag de la decoración que se va a ocultar
* `hide_now` - [*optional*] pasa True para ocultar una decoración de inmediato; con False se esperará al siguiente cambio de fondo o de escena.

Esta es la forma principal de ocultar una decoración. `hide_now` solo se recomienda en pruebas, ya que no disolverá las imágenes fuera de la escena.

<a id="mas_isdecotagenabled"></a>
### `mas_isDecoTagEnabled`
(**NEW in 0.12.3+**)

Parámetros:

* `tag` - (**REQUIRED**) image tag de la decoración de la que quieres comprobar si está habilitada

`RETURNS` True si la deco está habilitada, False si no

**Esto no significa que la decoración sea realmente visible en la imagen.** Esto comprueba si la decoración está configurada para mostrarse, pero, por el comportamiento del sistema, puede que la decoración real no sea visible para el usuario.

<a id="mas_isdecotagvisible"></a>
### `mas_isDecoTagVisible`
Parámetros:

* `tag` - (**REQUIRED**) image tag de la decoración de la que quieres comprobar la visibilidad

`RETURNS` True si la deco es visible, False si no

**Esto sí comprueba si la decoración es visible en la imagen.**
