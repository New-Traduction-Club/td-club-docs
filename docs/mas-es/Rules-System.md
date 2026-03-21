## Introducción

Desde la versión 0.7.4 existe un sistema de reglas para Event. Gracias a este sistema, la disponibilidad de un Event se decide comprobando las reglas que tenga asociadas.
Actualmente hay reglas de repetición por tiempo, reglas por rango de afecto y reglas especiales de probabilidad aleatoria para saludos y despedidas.

### Reglas de repetición

Estas reglas comprueban intervalos de tiempo para decidir si un Event puede repetirse.

#### MASNumericalRepeatRule 

Esta regla se define con la propiedad `repeat`, que marca el intervalo de repetición, y la propiedad `advance_by`, que indica cuántos intervalos se avanzan para programar la siguiente repetición. Está pensada para actualizar `start_date` y `end_date` del `Event` que la contiene y encajar bien con el sistema de calendario actual.

Ejemplo de funcionamiento:

Imagina que tenemos un `Event` programado para el 1 de enero de 2018. Si quieres que se repita el 1 de enero de 2019, basta con añadir una regla numérica con `repeat` en `year` y `advance_by` en 1. Si quisieras que se ejecutara cada dos meses, usarías `repeat` como `month` y `advance_by` como 2.

`repeat` solo acepta: "day", "week", "month" y "year".
`advance_by` acepta cualquier número entero mayor que 0.

Ejemplo de código:

``` renpy
init 5 python:
    rules = dict()
    rules.update(MASNumericalRepeatRule.create_rule(repeat=EV_NUM_RULE_YEAR))
    addEvent(
        Event(
            persistent.greeting_database,
            eventlabel="greeting_example", 
            start_date=datetime.datetime(2018, 2, 1),
            end_date=datetime.datetime(2018, 2, 2),
            unlocked=True, 
            rules=rules
        ),
        eventdb=evhand.greeting_database
    )
    del rules

label greeting_example:
    m "Oh, hello [player]!"
    m "This is just an example"

```

#### MASSelectiveRepeatRule

Esta regla se define mediante los parámetros `seconds`, `minutes`, `hours`, `days`, `weekdays`, `months`, `years`. Esos parámetros marcan rangos en los que el `Event` puede estar disponible. La regla puede comprobar la hora actual o cualquier otro momento concreto para ver si encaja en esos rangos.

Ejemplo de funcionamiento:

Imagina que quieres que un `Event` esté disponible solo de 9:00 a 16:59. Para ello, añade una regla selectiva con la propiedad `hours` en `[9,10,11,12,13,14,15,16]`. También puedes definir ese rango con `range`: `range(9,17)`, que suele ser más cómodo.

Esta regla no está limitada a una sola propiedad. Por ejemplo, si quieres que un `Event` solo esté disponible en viernes 13 de cualquier mes, puedes definir `days` como `[13]` y `weekdays` como `[4]` (los weekdays van de lunes = 0 a domingo = 6).

Cada propiedad se valida para aceptar únicamente intervalos de tiempo válidos.

Ejemplo de código en una despedida:
``` renpy
init 5 python:
    rules = dict()
    rules.update(MASSelectiveRepeatRule.create_rule(days=[13],weekdays=[4]))
    addEvent(
        Event(
            persistent.farewell_database,
            eventlabel="bye_special_friday",
            unlocked=True,
            rules=rules
        ),
        eventdb=evhand.farewell_database
    )
    del rules

label bye_special_friday:
    m "Bye [player]!"
    m "Example farewell"
    return 'quit'
```

### Regla de saludos

Para saludos hay una regla especial:

#### MASGreetingRule

Esta regla sirve para dos cosas: definir si el saludo debe omitir la inicialización visual y definir si tiene una probabilidad aleatoria especial de aparecer. Se configura con `skip_visual` y `random_chance`.

Ejemplo de código:
``` renpy
define opendoor.chance = 20

init 5 python:
    rules = dict()
    rules.update(
        MASGreetingRule.create_rule(
            skip_visual=True,
            random_chance=opendoor.chance
        )
    )
    addEvent(
        Event(
            persistent.greeting_database,
            eventlabel="i_greeting_monikaroom",
            unlocked=True,
            rules=rules
        ),
        eventdb=evhand.greeting_database
    )
    del rules

label i_greeting_monikaroom:
    #Some code for this special greeting
```

### Regla de despedidas

Para despedidas hay una regla definida:

#### MASFarewellRule

Esta regla solo define una probabilidad aleatoria especial para que la despedida esté disponible. La propiedad se llama `random_chance`.

Ejemplo de código:
``` renpy
init 5 python:
    rules = dict()
    rules.update(MASFarewellRule.create_rule(random_chance=10))
    addEvent(
        Event(
            persistent.farewell_database,
            eventlabel="bye_example",
            unlocked=True,
            rules=rules
        ),
        eventdb=evhand.farewell_database
    )
    del rules

label bye_example:
    m "Goodbye [player]!"
    return 'quit'
``` 

### Reglas basadas en afecto

Con la introducción del sistema de afecto en la versión 0.8.4, también podemos usar reglas según el estado de afecto actual de Monika.

En el momento de redactar esta guía, solo hay una regla de afecto.

#### MASAffectionRule

La regla se define con las propiedades `min` y `max`. Ambas aceptan un entero que define el afecto mínimo y máximo a partir del cual un Event se considera disponible, y ambos límites son inclusivos.
Para expresar un rango de "mayor que", define `min` con el umbral deseado y `max` como `None`.
Para expresar un rango de "menor que", define `min` como `None` y `max` con el umbral deseado.
No definas ambas como `None` al mismo tiempo, porque no habría umbral de afecto y la regla siempre daría disponibilidad positiva.

Ahora mismo, esta regla solo se comprueba para saludos y sirve únicamente para disponibilidad; **no**
fuerza la selección.

Ejemplo de código

``` renpy
init 5 python:
    rules = dict()
    rules.update(MASAffectionRule.create_rule(min=160,max=None))
    addEvent(
        Event(
            persistent.greeting_database,
            eventlabel="greeting_high_affection",
            unlocked=True,
            rules=rules
        ),
        eventdb=evhand.greeting_database
    )
    del rules

label greeting_high_affection:
    m "Welcome back my love!"
    return
```
