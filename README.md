# FNAS
Five Nights at Skibidi's

## Builds

| Archivo | Qué es |
|---|---|
| `fnaf release.html` | Versión final, **v3.0 «Señal Perdida»** |
| `fnas beta.html` | Periodo de beta de la v3.0: el mismo juego actualizado, con el aviso del equipo y las noches 1-4 abiertas |
| `fnas unreleased.html` | Compilación intermedia: noches 1-5 jugables y dificultad fijada en Normal |

`index.html` es la portada de GitHub Pages: lista sola los HTML y las carpetas del repositorio.

## Multimedia

Fuentes, imágenes, música y llamadas de teléfono **no** van incrustadas en el HTML: viven en
`assets/` y se sirven junto a la página.

```
assets/
  fonts/   Creepster y VT323 (.woff2)
  img/     logo del splash y periódico de la intro
  audio/   música del menú, clic y llamadas de cada noche
```

Consecuencia: los HTML ya no son archivos autónomos. Hay que jugarlos servidos por HTTP
(GitHub Pages lo hace solo); abiertos con `file://` no cargan la multimedia.
