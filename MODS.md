# Mods de Obsidiana

Un mod puede **agregar pueblos** a un periodo (o reemplazar uno), **vestirlos** y **cambiar la música** de una región.
Es un solo archivo de texto en formato JSON. No hace falta instalar nada: en el juego, abre **Comunidad**, pega el texto
del mod en **Mods** y pulsa **Revisar e instalar**. Funciona en la web, en el celular y en la computadora. El mod queda
guardado solo en tu dispositivo y se puede desactivar o quitar cuando quieras.

Ejemplo completo: [`mods/ejemplo_totonacas.json`](mods/ejemplo_totonacas.json). Agrega a los totonacas de Cempoala en
1519, con su atuendo.

## Lo que se revisa antes de instalar

Obsidiana es un juego de **historia real**, así que el juego revisa cada mod antes de instalarlo:

1. **Los campos obligatorios.** Cada pueblo trae su fuente (`fuente`: un libro, un artículo o un códice) y un dato
   histórico (`dato`).
2. **Que el juego conozca los valores.** La regla de poder, la clase de la unidad, el tipo de edificio, la economía y el
   aura del líder deben existir.
3. **Que se pueda jugar.** Con cada pueblo nuevo se prepara una partida de prueba y todos sus efectos deben aplicarse.

Si algo falla, el mod no se instala y el juego dice qué corregir.

## Formato

```json
{
  "id": "mi_mod",
  "nombre": "Nombre que se ve en la lista",
  "autor": "Tu nombre",
  "version": "1.0",
  "descripcion": "Qué agrega y por qué.",
  "culturas": { "s1500": [ { …un pueblo… } ] },
  "atuendos": { "culturas": { "id_del_pueblo": "estilo" }, "estilos": { … } },
  "musica": { "areas": { … }, "estilos": { … }, "familias": { … } }
}
```

- `id`: minúsculas, números y guiones bajos.
- Periodos: `cavernas`, `antiguedad`, `medieval`, `s1400`, `s1500`, `s1600`, `s1700`, `s1800` y `s1900_2000`.
- Para que tus pueblos no choquen con los del juego, ponles un `id` que empiece con `mod_`. Un pueblo con el mismo `id`
  que uno del juego lo **reemplaza**: sirve para proponer una versión corregida.

### Un pueblo

| Campo | Qué es |
| --- | --- |
| `id`, `nombre`, `lugar`, `fechas` | Identificador, nombre, sede y fechas |
| `coords` | `[longitud, latitud]` de su sede. Con ellas se eligen su área cultural, su paisaje, su ropa y su música |
| `poder` | `{nombre, texto, efectos, regla}`. Los efectos son los de `reglas.json` (p. ej. `"vida.infanteria": 0.1`) y la regla es una de las reglas de poder del juego |
| `unidad` | `{nombre, clase, texto, efectos}`. La clase es una de las del juego: `aldeano`, `infanteria`, `arqueria`, `caballeria`, `explorador`, `polvora`, `asedio`, `naval`, `sanador`, `blindado` o `aviacion` (que tenga sentido en su periodo) |
| `edificio` | `{nombre, texto, tipo}`. El tipo es `templo`, `consejo`, `mercado`, `trampa`, `casas`, `granero`, `vigia`, `muralla`, `cuartel`, `escuela`, `fundicion`, `astillero`, `campamento` o `estacion` |
| `maravilla` | Nombre de su gran obra |
| `lider` | `{nombre, titulo, texto, aura}`. El aura es `ataque`, `defensa`, `velocidad` o `curacion` |
| `colores` | Dos colores, como `["#e8d9a8", "#2f7d5a"]` |
| `recurso_clave`, `economia` | Recurso fuerte (`comida`, `madera`, `piedra`, `metal`, `riqueza`, `saber`, `petroleo`) y modelo económico (`agricola`, `comercio`, `tributo`, `minera`, `maritima`, `pastoral`, `recoleccion`, `forestal`, `saber`, `constructora`, `saqueo`, `industrial`) |
| `zona`, `escenario` | Opcionales: el paisaje sonoro y el escenario 3D de un pueblo del juego que se le parezca |
| `dato`, `fuente` | Un hecho histórico y de dónde sale |

Para copiar valores que sirven, lo más fácil es partir de un pueblo del juego que se le parezca.

### Atuendo

`atuendos.culturas` asigna a tu pueblo uno de los 58 estilos del juego (`mesoamerica`, `andes`, `japon`, `otomano`,
`llanuras`, `swahili`, `maori`…). Con `atuendos.estilos` puedes crear un estilo nuevo con la misma forma que los del
juego: tocados, prendas y piernas por papel y por época.

### Música

`musica.areas` y `musica.estilos` cambian qué familia musical suena en un área o en un estilo. `musica.familias` agrega
familias nuevas:

- escala en semitonos;
- `raiz` en Hz;
- `tempo`;
- `lider` y `segundo`, con un instrumento de síntesis cada uno: `soplo`, `pulsada`, `arco`, `lengueta`, `metal`,
  `kalimba` o `voz`;
- `bordon`: `tanpura`, `didgeridoo`, `garganta`, `arco` o `gaita`;
- percusión `calma` y `tensa` en patrones de 16 pasos (`X` fuerte, `x` media, `o` suave, `.` silencio);
- `cuerno`, la llamada de guerra.

## Compartir tu mod

Abre una propuesta con la plantilla **Compartir un mod** en
[github.com/jfrodriguezva/Obsidiana/issues](https://github.com/jfrodriguezva/Obsidiana/issues) y pega ahí el texto.
Los mods que se revisan con fuentes pueden entrar al juego.

## Retos

En **Comunidad → Retos**, «Crear reto con lo elegido» genera un código (`OBS1-…`) con el periodo, los pueblos, la
semilla del mapa, la dificultad y las opciones. Quien lo pegue juega exactamente la misma partida. En la web también
sirve como enlace: `https://jfrodriguezva.github.io/Obsidiana/?reto=OBS1-…`.
