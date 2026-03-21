# API Keys

## Cómo funcionan las claves

Cada clave se define mediante un "nombre de funcionalidad" que **debe** ser único.
Las claves se cargan en el nivel de init -980. **Las claves de API NO se guardan en `persistent`.**
Se leen desde un archivo JSON independiente llamado `api_keys.json`, ubicado en la misma carpeta en la que se guardan los datos persistentes.
Si acabas de empezar con esto, no te preocupes: para consultar y usar claves de API, revisa la API que tienes abajo.

## API 

[arriba](#api-keys)
### `mas_getAPIKey`
Obtiene la clave de API de una funcionalidad concreta.

Parámetros:

- `feature` - nombre en formato string de la funcionalidad cuya clave de API quieres obtener

DEVUELVE la clave de API como string si se encuentra; string vacío si no se encuentra

[arriba](#api-keys)
### `mas_hasAPIKey`
Comprueba si una funcionalidad tiene una clave de API registrada.

Parámetros:

- `feature` - nombre en formato string de la funcionalidad para la que se comprueba la clave de API

DEVUELVE true si la funcionalidad tiene una clave de API; false en caso contrario

[arriba](#api-keys)
### `mas_registerAPIKey`
Registra una clave de API para una funcionalidad concreta.

Parámetros:

- `feature` - nombre en formato string de la funcionalidad para la que se registra la clave de API
- `display_name` - nombre que la funcionalidad debe usar cuando se muestre en la pantalla de claves de API
- `on_change` - función que se ejecuta cuando cambia la clave de API (incluye tanto añadir como eliminar una clave)
    - Valor por defecto: `None`
