# FNAS
Five Nights at Skibidi's

> ### ⚠️ Fangame sin ánimo de lucro
> Proyecto de fans, **gratuito y no comercial**. No es un producto oficial ni está
> afiliado, patrocinado o respaldado por **Scott Cawthon** (*Five Nights at Freddy's*)
> ni por **DaFuqBoom** (*Skibidi Toilet*).

## Cómo jugar

**🌐 Solo se puede jugar en la web oficial:** <https://pineappleva.github.io/FNAS/>

Descargar el HTML **no funciona**. El juego necesita servir la carpeta `assets/`
por HTTP desde el mismo sitio que la página: si abres el fichero descargado con
doble clic (`file://`), no carga ni las fuentes, ni las imágenes, ni la música, ni
las llamadas de teléfono. Es así a propósito: la copia de referencia es la que
está publicada, no la que alguien se baje.

Si quieres el código para estudiarlo o modificarlo, clona el repositorio y sírvelo
con cualquier servidor local (`python3 -m http.server`, por ejemplo).

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
  fonts/   Creepster y VT323 (.woff2) + su licencia OFL
  img/     logo del splash y periódico de la intro
  audio/   música del menú, clic y llamadas de cada noche
```

Consecuencia: los HTML ya no son archivos autónomos. Por eso el juego solo funciona servido
desde la web oficial —ver [Cómo jugar](#cómo-jugar).

## Créditos y recursos de terceros

| Recurso | Titular |
|---|---|
| Audio e imágenes procedentes de *Five Nights at Freddy's* | **Scott Cawthon**, creador del juego original |
| Universo, personajes y marca *Skibidi Toilet* | **DaFuqBoom** |
| Tipografía *Creepster* | © 2011 Font Diner, Inc — SIL Open Font License 1.1 |
| Tipografía *VT323* | © 2011 The VT323 Project Authors — SIL Open Font License 1.1 |
| Código del juego | Jaime Gaming · Equipo Pineapple |

El detalle archivo por archivo está en [`assets/README.md`](assets/README.md).

## Licencia

Este repositorio tiene **dos regímenes distintos**, y es importante no confundirlos:

- ✅ **El código** —HTML, CSS y JavaScript de los builds— es software libre bajo la
  **MIT License**: ver [`LICENSE`](LICENSE). Puedes usarlo, modificarlo y redistribuirlo.
- ❌ **La multimedia no.** Todo lo que hay en [`assets/`](assets/) —audio, imágenes y
  cualquier otro recurso de terceros— queda **excluido** de esa licencia. No somos sus
  titulares y no tenemos derecho a sublicenciarlo ni a redistribuirlo, así que no podemos
  concederlo. Ver [`NOTICE`](NOTICE).

**Si reutilizas el código:** hazlo bajo la MIT, pero **no redistribuyas la carpeta
`assets/`** junto a él. Retírala y usa recursos propios o con licencia compatible.

## Sin monetización

Este proyecto es y seguirá siendo **100 % gratuito**: sin micropagos, sin publicidad, sin
enlaces de donación y sin venta en ninguna plataforma. Es la condición bajo la que la
comunidad de FNAF puede trabajar con los recursos del juego original.
