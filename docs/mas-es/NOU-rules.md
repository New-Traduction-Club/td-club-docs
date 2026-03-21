### Cómo desbloquear

Recibirás una pista dentro del juego y, después, aparecerá una carta con las instrucciones en la carpeta `characters/`.

### Conceptos básicos de NOU

- El objetivo es jugar todas tus cartas antes que tu oponente.
- Cada ronda te da una cantidad de [puntos](./NOU-rules.md#tabla-de-valor-de-cartas) según las cartas que le queden al oponente.
  - Es posible ganar una ronda y no obtener puntos, y viceversa: perderla sin ceder ningún punto.
  - La primera persona en alcanzar la meta de puntos (200 por defecto) gana la partida.
- **Antes** de jugar tu penúltima carta (es decir, al moverla a la pila de descarte), debes decir "NOU".
  - Si se te olvida, la otra persona puede pillarte por no decir "NOU" y hacerte robar 2 cartas.
  - Solo puedes pillar a alguien **antes** de jugar tu propia carta.
- Si no puedes (o no quieres) jugar una carta en tu turno, debes robar una de la pila de robo.
  - No estás obligado a jugar la carta robada; puedes pasar el turno después.
- Por defecto, los jugadores pueden [reflejar](./NOU-rules.md#tabla-de-reflejo-de-cartas) (ojo: **no** acumular) algunas cartas de acción si tienen las cartas adecuadas.
- Por defecto, solo puedes jugar *Roba 4* cuando no tienes cartas del color actual de la pila de descarte.

#### Tabla de valor de cartas

| Cartas numéricas | Cartas de acción | Comodines |
| :--------------: | :--------------: | :-------: |
| 0-9              | 20               | 50        |

#### Tabla de reflejo de cartas

| ↓ se puede reflejar con → | Reversa    | Salto       | Roba 2      | Roba 4 |
| :-----------------------: | :--------: | :---------: | :---------: | :----: |
| Reversa                   | cualquiera |             |             |        |
| Salto                     |            | mismo color |             |        |
| Roba 2                    |            |             | cualquiera  |        |
| Roba 4                    |            |             | mismo color |        |

### Reglas de la casa de NOU

Es posible ajustar algunos elementos de la partida.

* Puedes cambiar los puntos de victoria (el objetivo para ganar la partida).
  * Valor predeterminado: 200
* Puedes cambiar el número de cartas iniciales.
  * Valor predeterminado: 7 cartas
* Puedes jugar con *Roba 2 acumulables* (cada reflejo de *Roba 2* —o de *Roba 4*— se suma a las cartas anteriores); la última persona acaba robando todas las cartas.
  * Valor predeterminado: `False`
* Puedes jugar con *Roba 4 sin restricción*, lo que permite jugar *Roba 4* en cualquier momento, incluso si tienes una carta del color actual.
  * Valor predeterminado: `False`
* *Caos de reflejo* hace la partida más caótica al facilitar los reflejos ([consulta aquí](./NOU-rules.md#tabla-de-reflejo-de-cartas-solo-con-caos-de-reflejo-activado)).
  * Puedes reflejar cualquier *Salto* con un *Salto* de cualquier color.
  * Puedes reflejar un *Roba 2* con un *Roba 4*.
  * Puedes reflejar un *Roba 4* con un *Roba 4*.
  * Valor predeterminado: `False`

#### Tabla de reflejo de cartas (solo con Caos de reflejo activado)

| ↓ se puede reflejar con → | Reversa    | Salto      | Roba 2      | Roba 4     |
| :-----------------------: | :--------: | :--------: | :---------: | :--------: |
| Reversa                   | cualquiera |            |             |            |
| Salto                     |            | cualquiera |             |            |
| Roba 2                    |            |            | cualquiera  | cualquiera |
| Roba 4                    |            |            | mismo color | cualquiera |

### API de reglas de la casa de NOU

#### Claves usadas actualmente:
* `points_to_win`
* `starting_cards`
* `stackable_d2`
* `unrestricted_wd4`
* `reflect_chaos`

#### Funciones:
* `mas_nou.get_house_rule` - devuelve el valor de una regla de la casa
* `mas_nou.set_house_rule` - establece un valor nuevo para una regla de la casa
* `mas_nou.reverse_house_rule` - (SOLO PARA BOOLEANOS) invierte una regla de la casa
* `mas_nou.get_default_house_rules` - devuelve un `dict` con las reglas de la casa predeterminadas y sus valores
* `mas_nou.are_default_house_rules` - comprueba si las reglas actuales son las predeterminadas
* `mas_nou.update_house_rules` - (SOLO PARA ACTUALIZACIONES, NO LA LLAMES CONSTANTEMENTE, ESPECIALMENTE CON `force=True`) puede usarse para actualizar la persistencia en caso de que se añada una regla de la casa nueva
