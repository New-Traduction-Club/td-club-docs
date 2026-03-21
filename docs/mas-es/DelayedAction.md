# Resumen

El framework DelayedAction permite poner en cola acciones basadas en `Event`, además de acciones personalizadas, y ejecutarlas más adelante cuando se cumpla una condición. **Esto NO sustituye la comprobación condicional de Event.** Está pensado sobre todo para ejecutar código que depende de variables del sistema o de condiciones iniciales.

# Componentes

El framework DelayedAction se compone de lo siguiente:

* clase `MASDelayedAction`
* store `mas_delact` (módulo que centraliza guardado y carga)

## MASDelayedAction

Esta clase incluye varias propiedades, pero las principales son estas (todas obligatorias en el constructor):

* id - ID único de esta DelayedAction
* ev - `Event` asociado a esta DelayedAction
* conditional - condición evaluada con `eval` que controla cuándo se ejecuta la DelayedAction
* action - una constante `EV_ACTION` o un callable que realiza la acción
* flowcheck - constante `MAS_FC` que define en qué momento se comprueba la condición

Esta clase también incluye un método estático `makeWithLabel`, que puede crear una instancia de DelayedAction usando un `eventlabel` en lugar del `event` real. Esto asume que `mas_getEV` está disponible, así que asegúrate de usar el nivel de init adecuado.

Las DelayedActions están pensadas para actuar como wrappers de acciones comunes y permitir su ejecución diferida cuando se cumpla `conditional`, en momentos concretos del inittime o runtime, incluso varias sesiones después.

Cuando se cumple la condición de una DelayedAction, se ejecuta la acción. Si la acción termina correctamente, se elimina del mapa de DelayedAction y de la lista de acciones diferidas de `persistent`.

Las acciones que sean callables deben devolver `True` en caso de éxito y `False` en caso contrario, para indicar al framework si la acción se completó correctamente. Las acciones callables se invocan con el objeto `Event` mediante la keyword `ev`.

Flowcheck está diseñado para funcionar con comprobación bit a bit, así que una DelayedAction puede comprobarse en varios lugares combinando con OR bit a bit las constantes `MAS_FC`.

## mas_delact

Este store contiene funciones de guardado/carga para el mapa de DelayedAction, además de `MAP`, que relaciona IDs de DelayedAction con funciones constructoras.

# Configuración

Para configurar una DelayedAction, necesitas lo siguiente:

1. Una función constructora que pueda crear una DelayedAction en el nivel de init 994.
2. Un `Event` sobre el que ejecutar la DelayedAction.

Y para crearla:

1. Crea una función constructora para generar la DelayedAction. Esta función debe llevar prefijo de un único guion bajo y definirse en el store `mas_delact`. Este store tendrá acceso al import `store`, así que podrás recuperar desde aquí el resto de variables. Debes crear esta función en un nivel de init anterior a 994. Esta función no debe aceptar parámetros y debe devolver un objeto `MASDelayedAction`.
2. Añade esa función al diccionario `mas_delact.MAP` ubicado en `event-handler.` Asegúrate de que tu ID sea único y coincida con el que usaste al crear el objeto `MASDelayedAction`. Se recomienda usar un número como ID.
3. Llama a `mas_addDelayedAction` usando el ID de tu DelayedAction cuando necesites ponerla en cola.

# Ejecución

Así funciona la ejecución de DelayedAction:

1. En el nivel de init 994, todos los IDs de DelayedAction guardados en `persistent._mas_delayed_action_list` se convierten en instancias de DelayedAction y se almacenan en `mas_delayed_action_map`. Ten en cuenta que esta variable de runtime es un diccionario, mientras que la variable de `persistent` es una lista.
2. En el nivel de init 995, se comprueban todas las DelayedActions cuyo `flowcheck` contiene `MAS_FC_INIT`, y se ejecutan si se cumple la condición.
3. Las DelayedActions cuyo `flowcheck` contiene `MAS_FC_START` se comprueban durante runtime en splash.
4. Las DelayedActions cuyo `flowcheck` contiene `MAS_FC_IDLE_ONCE` se comprueban durante runtime en `ch30_preloop`.
5. Las DelayedActions cuyo `flowcheck` contiene `MAS_FC_IDLE_ROUTINE` se comprueban aproximadamente una vez por minuto en `ch30_loop`.
6. Las DelayedActions cuyo `flowcheck` contiene `MAS_FC_END` se comprueban durante runtime en `quit`.
7. Los IDs de las DelayedActions que no se ejecutaron en esta sesión se guardan en `persistent._mas_delayed_action_list`. **NOTA: Esta lista siempre se regenera; no se añade al final al cerrar la sesión.**

# Adicional

Todo el código de DelayedAction está en `event-handler.`

El primer `Event` que usó DelayedActions fue el evento de las islas. Se utilizó para gestionar casos en los que no se podían decodificar imágenes, lo que implicaba que el `Event` debía seguir bloqueado hasta que esas imágenes se analizaran correctamente.
