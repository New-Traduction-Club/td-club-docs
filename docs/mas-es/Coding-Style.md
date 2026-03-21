# Estilo de Código

**NO CAMBIES CÓDIGO EXISTENTE SOLO POR CAMBIAR EL ESTILO**

Si vas a editar de forma significativa código ya existente, entonces sí está bien ajustar el estilo. En caso contrario, mantén cualquier añadido coherente con el código cercano.
Los cambios que son únicamente de estilo desperdician recursos y faltan al respeto a la persona que escribió el código original; cualquier cambio de ese tipo se deshará o se rechazará.
Esto incluye, entre otras cosas:

* añadir/eliminar líneas en blanco
* cambiar el estilo de comentarios
* cambiar el estilo de salto de línea
* cambiar la indentación (excepto en errores de sintaxis)

Por lo demás, no tenemos una guía de estilo estricta, pero aquí tienes algunas convenciones
que nos gusta seguir:

### Indentación

**Sangría de cuatro espacios.**

### Labels

Los nombres de label deben ir en minúsculas y separados por guiones bajos (`monika_twitter`).
Si usas muchos labels para un subprograma relacionado, ponles el prefijo `mas` y el
nombre de tu subprograma (p. ej.: `mas_coolfungame_flowstart`). **Excepciones a
esta regla:** los temas/saludos/despedidas de Monika, aunque esto podría cambiar en
el futuro.

Algunos prefijos están reservados:

- `greeting` - se usa para saludos normales
- `i_greeting` - se usa para saludos interactivos especiales
- `ch30` - se usa para labels clave del capítulo 30
- `monika` - se usa para casi todos los temas de Monika
- `m_joke` - también se usa para el sistema de chistes
- `mas_poem` - se usa para el sistema poemgame
- `mas_compliment` - se usa para cumplidos
- `mas_mood` - se usa para estados de ánimo
- `mas_story` - se usa para historias
- `mas_apology` - se usa para disculpas no genéricas
- `mas_song` - se usa para canciones (añade el sufijo `_long` para canciones largas)
- `game` - se usa para la mayoría de minijuegos
- `vv` - se usa para contenido relacionado con actualizaciones
- `v` - también se usa para contenido relacionado con actualizaciones
- `bye` - se usa para despedidas

Puede haber más, así que en general ten cuidado con los labels que uses.


### Store

En Renpy, los stores son como espacios de nombres, salvo que no puedes anidarlos.
Recomendamos agrupar datos relacionados, constantes y funciones en stores para evitar
ensuciar el espacio de nombres global.

Para crear un store:
```python
init python in mas_store_name:
    var1 = 1
    var2 = 2
    ...

# or
define mas_store_name.var1 = 1
define mas_store_name.var2 = 2
```

Para acceder a un store:
```python
store.mas_store_name.var1 = 1

# or
python:
    import store.mas_store_name as mas_store_name
    mas_store_name.var1 = 1
```

Usamos varios stores distintos para agrupar diferentes datos. Cuando decidas crear
un store nuevo, asegúrate de que no exista ya uno en uso. Pon a tus stores el
prefijo `mas_`.

`persistent` es como un store, pero especial porque se guarda en disco.
**Úsalo solo si necesitas guardar datos entre varias sesiones**
Más sobre esto más adelante...

### Funciones

Si una función es muy específica de un subprograma o flujo, considera crearla en
un store e importarla cuando haga falta. Si una función puede generalizarse para
muchos casos de uso, entonces créala en un bloque `init python` normal (lo que la
hace global). **Pon el prefijo mas a las funciones globales**

Para documentación, están bien tanto comentarios de bloque (`#`) como docstrings (`"""`).
No imponemos una forma concreta de documentar funciones, pero indicar qué hace
la función, sus variables de entrada y salida, qué devuelve y qué variables asume
es un buen comienzo:

```python
def mas_someKindOfFunction(var1, var2, var3=None):
    """
    This function does some kind of thing. Use with caution.

    IN:
        var1 - value of something
        var3 - like the most value of something
            (Default: None)

    OUT:
        var2 - contains modified reference to something

    RETURNS:
        a copy of var2

    ASSUMES:
        persistent.var4
    """
```
Para nombres de funciones, valen tanto camelCase como lowercase_underscores.

### Persistent

Este elemento tipo store guarda datos en disco y es como renpy hace seguimiento de datos.
Como ya viene cargado con datos del juego base, **evita usarlo si puedes**.
(P. ej.: en lugar de usar un persistent para comprobar si se vio un evento,
usa `renpy.seen_label` o `seen_event`.

**Pon el prefijo `_mas_` a todas las variables persistent.** (Ahora mismo
estamos en proceso de convertir todos los valores de `persistent` ya creados
para que estén prefijados correctamente)

### Constantes

Define constantes en lugar de literales cuando las uses varias veces.
Usa UPPERCASE_UNDERSCORES para nombrarlas.

**Una excepción son los literales usados en screens**. Si una screen **no**
se llama con `nopredict`, entonces usa literales cuando puedas, porque renpy
optimiza las screens con literales.

### Variables

Hazlas descriptivas, por favor. No hace falta llegar al estilo Java; basta con
que sea razonablemente fácil entender qué son. Abreviaturas o acrónimos están
bien. Usa lowercase_underscores para nombrarlas.

### Comentarios

Por favor, escribe comentarios. Aunque python ya sea legible, conocer el motivo
de alto nivel de lo que hacemos o los efectos de alto nivel de hacerlo ayuda.

### Longitud de línea

De nuevo, no se aplica estrictamente, pero mantenlas en algo razonable. Personalmente
las limito a 80 columnas, pero llegar a 120 probablemente está bien.
**La excepción es el código Renpy.** El código Renpy no siempre puede dividirse
en varias líneas.

### Assets

Cualquier asset que uses debe estar en la carpeta `mod_assets/`. Si tienes muchos
assets, agrúpalos en una subcarpeta.

### Paquetes de terceros

Si puedes hacerlo sin usar un paquete externo, hazlo sin el paquete externo.
Las excepciones deben discutirse con el equipo de desarrollo. Si la librería que
quieres añadir pesa más de un megabyte, casi seguro que **no** se permitirá.
