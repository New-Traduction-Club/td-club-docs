# Decorators

Estos son los decorators (funciones que envuelven otras funciones o clases para cambiar su comportamiento) estándar disponibles en el mod.

[arriba](#decorators)
### `mas_reset.ch30_reset`
Marca una función para que se ejecute durante `ch30_reset`.
Debe usarse para inicializar o restablecer el estado de Monika.

Parámetros:

- `priority` - define el orden de ejecución de la función. Una prioridad más baja se ejecuta antes.
    - **USA PRIORIDADES >= 0, POR FAVOR**. Si necesitas colocar algo entre el código de reset que ya existe, revisa `script-ch30` para ubicarlo correctamente.
    - Valor por defecto: 0

[arriba](#decorators)
### `mas_utils.deprecated`
Marca funciones y clases como obsoletas (siguen funcionando, pero se desaconseja usarlas en código nuevo).

Parámetros:

- `use_instead` - string (cadena de texto) con el nombre de la función/clase que debe usarse en su lugar
    - Valor por defecto: `None`
- `should_raise` - bool (valor lógico `True`/`False`) que determina si usar esta función o clase lanza una excepción (error que interrumpe la ejecución)
    - Si es True, lanzará una excepción cuando se use la función
    - Valor por defecto: `False`

[arriba](#decorators)
### `mas_submod_utils.functionplugin`
Marca una función para que se ejecute cuando se ejecute una label (etiqueta de Ren'Py) u otra función.
Básicamente, te permite engancharte a cualquier elemento que sea una label o función.

Parámetros:

- `_label` - la label o función a la que engancharse
- `_args` - lista de argumentos para pasar a la función marcada
    - Valor por defecto: `[]`
- `auto_error_handling` - bool que determina si las excepciones se capturan y registran en vez de lanzarse
    - Si es True, capturará las excepciones y las registrará en `mas_log`
    - Valor por defecto: `True`
- `priority` - define el orden de ejecución de la función. Una prioridad más baja se ejecuta antes.
    - Valor por defecto: 0
