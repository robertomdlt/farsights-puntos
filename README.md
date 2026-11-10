# farsights-puntos

Datos públicos que usa la app [FarSights](https://robertomdlt.github.io/farsights-legal/) para no depender
de servidores saturados. Se sirven a la app a través de [jsDelivr](https://www.jsdelivr.com/). Las cumbres
están en [farsights-datos](https://github.com/robertomdlt/farsights-datos).

## `pois/v1/`

Refugios, abrigos, fuentes de agua potable y manantiales de OpenStreetMap, en cuadrículas de 1° × 1°. Los
aparcamientos no están (son demasiados): la app los pide a OpenStreetMap (Overpass).

- `index.json`: versión, fecha de generación y lista de cuadrículas cubiertas.
- `<lat>_<lon>.json`: esquina suroeste de la cuadrícula en grados enteros (`40_-4` = 40–41° N, 4–3° O).
  Lista de puntos con claves cortas:
  - `i` id de OpenStreetMap con su tipo (`n123` nodo, `w123` vía; las vías van en el centro de su recuadro)
  - `k` tipo: `h` refugio guardado (`tourism=alpine_hut`), `f` refugio libre (`tourism=wilderness_hut`,
    `shelter_type=basic_hut`), `s` abrigo (`shelter_type=lean_to|rock_shelter`), `w` fuente
    (`amenity=drinking_water`, o `fountain` con `drinking_water=yes`), `p` manantial (`natural=spring`)
  - `a`, `o` latitud y longitud
  - `n` nombre y `l` nombres en otros idiomas que difieren de `n` (opcionales)
  - `c` plazas (opcional), `d` agua potable 1 sí / 0 no (sin `d`, no se sabe), `e` 1 si puede secarse

  Una cuadrícula cubierta sin puntos es `[]`. Solo hay ficheros para las cuadrículas cubiertas del todo por los
  datos descargados; para las demás, la app pregunta a OpenStreetMap (Overpass).

Regiones (v1.0): todo el mundo (Geofabrik por continentes).

Se generan con `scripts/build-poi-tiles.mjs` del repositorio de la app.

## Licencia

Los datos son © colaboradores de OpenStreetMap y están disponibles bajo la
[Open Database License (ODbL)](https://opendatacommons.org/licenses/odbl/). Ver https://www.openstreetmap.org/copyright.
