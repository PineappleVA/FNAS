# `assets/` — recursos multimedia

> ⚠️ **Esta carpeta NO está cubierta por la licencia del código.**
> El `LICENSE` (MIT) de la raíz se aplica solo al HTML/CSS/JS del proyecto.
> Nada de lo que hay aquí puede redistribuirse bajo esa licencia: no somos sus
> titulares y no tenemos derecho a cederlo. Detalles en [`../NOTICE`](../NOTICE).

Contenido servido junto a las páginas: los tres builds lo cargan con rutas
relativas (`assets/...`), ya no va incrustado en base64 dentro del HTML.

## Procedencia

| Archivo | Contenido | Procedencia / licencia |
|---|---|---|
| `fonts/creepster-400.woff2` | tipografía Creepster | © 2011 Font Diner, Inc · **SIL OFL 1.1** → [`fonts/OFL.txt`](fonts/OFL.txt) |
| `fonts/vt323-400-latin.woff2`<br>`fonts/vt323-400-latin-ext.woff2` | tipografía VT323 (subconjuntos latin y latin-ext) | © 2011 The VT323 Project Authors · **SIL OFL 1.1** → [`fonts/OFL.txt`](fonts/OFL.txt) |
| `img/splash-logo.png` | logo del splash («Pineapple presenta») | Equipo Pineapple · obra propia |
| `img/newspaper-intro.png` | periódico «Skibiry Herald» de la intro | Scott Cawthon · obra mixeada |
| `audio/title-theme.m4a` | música de la pantalla de título | Scott Cawthon · obra propia |
| `audio/click.mp3` | clic de interfaz | Equipo Pineapple · obra propia |
| `audio/phone/night1-4.mp3` | llamadas de teléfono de cada noche (builds v3.0: `fnaf release.html` y `fnas beta.html`) | Equipo Pineapple · obra propia |
| `audio/phone-unreleased/night1-4.mp3` | llamadas de teléfono de la compilación Unreleased | Equipo Pineapple · obra propia |

**Regla general:** mientras una fila no esté confirmada como obra propia, el
archivo se trata como recurso de terceros y queda **excluido** de la licencia
del código. Las filas marcadas con ⚠️ son las que el equipo debe revisar y
completar; si un recurso resulta ser propio, basta con cambiar su fila.

Los binarios idénticos entre builds se guardan una sola vez y se comparten:
el logo, el periódico, la música del título y el clic son los mismos ficheros
para las tres versiones.

## Atribución obligatoria

- Los recursos de audio e imagen procedentes de *Five Nights at Freddy's*
  pertenecen a **Scott Cawthon**, creador del juego original.
- El universo, los personajes y la marca *Skibidi Toilet* pertenecen a
  **DaFuqBoom**.
- Este proyecto es un **fangame gratuito y sin ánimo de lucro**, no oficial y
  sin afiliación, patrocinio ni respaldo de ninguno de los dos.

## Sin monetización

Ningún recurso de esta carpeta puede usarse en una versión de pago, con
publicidad, con micropagos o con enlaces de donación. Es la condición bajo la
que la comunidad de FNAF puede trabajar con los recursos del juego original.

## Añadir recursos nuevos

1. Comprueba que tienes derecho a usarlos (obra propia, licencia compatible o
   recurso del juego original dentro de un fangame sin ánimo de lucro).
2. Añade la fila correspondiente en la tabla de procedencia de arriba.
3. Si trae su propia licencia (como las tipografías OFL), incluye el texto en
   esta carpeta, igual que `fonts/OFL.txt`.
