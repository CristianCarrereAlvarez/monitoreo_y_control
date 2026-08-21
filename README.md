# monitoreo_y_control

Repositorio de control del sistema de monitoreo de Cristián Carrère
(cristian@espaciotp.cl). Acá vive lo que **se puede versionar**: hoy, el
prompt de la rutina semanal.

---

## Qué hay acá, y por qué

```
prompts/
  monitoreo-semanal.md   ← el prompt de la Routine «Monitoreo Semanal»
  trigger-stub.md        ← el reemplazo del contenido del trigger, aún no desplegable
```

`prompts/monitoreo-semanal.md` es la **fuente canónica** del prompt que ejecuta
la rutina de los lunes. La copia que corre vive dentro del trigger
`trig_01RTagcd3J82T42seo9C4Kp7` y es un **despliegue** de este archivo.

`prompts/trigger-stub.md` es el diseño que reemplazaría a esa copia: un texto
corto que manda a leer el prompt acá con el conector de GitHub. **Todavía no se
puede usar** — ver más abajo.

**Por qué existe este repositorio.** El prompt tiene ~56 KB, se reescribió
ocho veces en un solo día, y hasta el 20-08-2026 su única copia vivía dentro
del trigger: sin historial, sin diff, y sin nada a qué volver si una edición
lo rompía. Eso se acabó.

---

## La regla, que es lo único que impide tener dos versiones

**Todo cambio se escribe primero acá, se commitea, y recién entonces se
despliega al trigger.** Nunca al revés, y nunca solo en uno de los dos.

El orden importa. Un cambio hecho solo en el trigger no deja rastro: no hay
commit, no hay diff, y la próxima vez que alguien lea este archivo va a creer
que es lo que está corriendo. Un cambio hecho solo acá no corre.

## Por qué el trigger todavía no es un stub

La regla de arriba tiene un defecto conocido: depende de que alguien se acuerde
del segundo paso. El 20-08-2026 no se acordó, y las dos copias quedaron
separadas una noche entera, con v14 acá y v13 corriendo. La corrección obvia es
sacar el segundo paso: dejar el prompt solo acá y que el trigger no contenga
instrucciones sino la orden de venir a leerlas con el conector de GitHub. Ese
texto está escrito, en `prompts/trigger-stub.md`.

**No se puede desplegar todavía, y está medido.** El 21-08-2026 se disparó el
propio trigger semanal con un prompt de prueba que solo intentaba leer este
archivo. Respondió:

```
RESULTADO: NO
HERRAMIENTA: no disponible
ERROR: el conector de GitHub no está conectado en esta sesión; get_file_contents
       no aparece entre las disponibles (servidores MCP presentes: Gmail, Notion,
       Spotify, Undermind, Google Drive, Google Calendar, claude-code-remote)
```

La sesión que abre la tarea programada **no tiene GitHub**. Un stub que mandara
a leer el repositorio produciría cero informes: el propio stub detectaría el
fallo y mandaría el correo de aviso, que es mejor que colgarse en silencio,
pero no es un monitoreo.

**Qué lo desbloquea:** habilitar el conector de GitHub en los conectores de la
Routine, desde la interfaz de Routines de claude.ai. Un trigger creado o
editado por herramienta solo puede heredar los conectores que tenga la sesión
que lo edita, y esta no tiene GitHub para pasar. Cuando esté habilitado, se
vuelve a correr la misma prueba y, si da SÍ, se pega el stub.

### Qué versión corrió

La primera línea del prompt declara la versión:

```
VERSIÓN v16 · 2026-08-21 · fuente canónica: ...
```

El prompt obliga a copiarla en el bloque 12 del informe semanal. Entonces el
chequeo es trivial y no requiere abrir el trigger:

> ¿la versión que declara el Doc del lunes es la misma que la del último commit
> de este archivo?

Si no coincide, alguien editó una copia y no la otra. Al subir un cambio, sube
el número de versión y la fecha de esa primera línea.

## Qué NO está acá, y dónde está

El sistema no es código. Casi todo vive fuera de git, y duplicarlo acá
crearía exactamente el problema que este repositorio existe para evitar:

| qué | dónde vive |
|---|---|
| Flujo de Registro (las siete fases, las tres capas, los puntos de control) | Notion, página `3c18ae9c-ac0a-8173-bae8-e4869b37efc7` |
| Protocolo de archivos y carpetas | Notion, página `3c18ae9c-ac0a-81ea-b30e-ef35516d15e7` |
| Personas, Organizaciones, Portafolio, Oportunidades, Competencias, Evidencia | Notion |
| Carta de Navegación | Google Drive, `1ZrYE8gs46qEECnBuU_846IGSbyTS0xLGo5xhzVa0irk` — **solo lectura** |
| Informes semanales, bitácoras, entregables | Google Drive |
| Los eventos y recordatorios | Google Calendar |

Esas páginas de Notion las edita Cristián a mano y son la fuente de sí
mismas. **No se copian acá.**

---

## Historial

- **v16 · 2026-08-21** — deja escrito, en el §4 y en el §3, que la sesión del
  trigger no tiene el conector de GitHub, medido ese día sobre el propio
  trigger. v15 había dado por hecho lo contrario y quedó sin desplegar.
- v9–v14 · 2026-08-20 — ver `git log`.
- **v8 · 2026-08-20** — primera versión versionada. Corrige cinco valores de
  `Fuerza del vínculo` y `Tipo de vínculo` que el prompt nombraba y que no
  existían en Notion; incorpora la regla de git; obliga a declarar la versión
  en el bloque 12.
- v1–v7 — anteriores al repositorio. No hay historial: vivieron solo dentro
  del trigger. v7 es la que corrió hasta el 20-08-2026.
