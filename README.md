# monitoreo_y_control

Repositorio de control del sistema de monitoreo de Cristián Carrère
(cristian@espaciotp.cl). Acá vive lo que **se puede versionar**: hoy, el
prompt de la rutina semanal.

---

## Qué hay acá, y por qué

```
prompts/
  monitoreo-semanal.md   ← el prompt de la Routine «Monitoreo Semanal»
  trigger-stub.md        ← lo único que vive dentro del trigger
```

`prompts/monitoreo-semanal.md` **es** el prompt que ejecuta la rutina de los
lunes. No una fuente de la que se saca una copia: el archivo mismo. El trigger
`trig_01RTagcd3J82T42seo9C4Kp7` no contiene instrucciones — contiene la orden
de leer este archivo con el conector de GitHub y seguirlo. Ese texto es
`prompts/trigger-stub.md`, y también está versionado.

**Por qué existe este repositorio.** El prompt tiene ~56 KB, se reescribió
ocho veces en un solo día, y hasta el 20-08-2026 su única copia vivía dentro
del trigger: sin historial, sin diff, y sin nada a qué volver si una edición
lo rompía. Eso se acabó.

---

## Ya no hay dos versiones que sincronizar

**Un commit en `main` es un despliegue.** No hay segundo paso, no hay copia
que actualizar, y no existe manera de cambiar lo que corre el lunes sin dejar
historial. Editar el prompt es editar este archivo.

**Por qué se hizo así el 21-08-2026.** Antes había dos copias y una regla:
escribir primero acá, commitear, y recién entonces desplegar al trigger. La
regla era correcta y aun así el 20-08-2026 las dos copias quedaron separadas
una noche entera —v14 acá, v13 corriendo—, porque un mecanismo que depende de
acordarse del segundo paso falla el día que alguien no se acuerda. La versión
correcta de esa regla no era vigilarla mejor: era sacar el segundo paso.

El trigger quedó reducido a `prompts/trigger-stub.md`, que hace dos cosas:
manda a leer `prompts/monitoreo-semanal.md` con el conector de GitHub, y dice
qué hacer si no lo consigue — mandar un correo diciendo que no corrió, y no
ejecutar nada. Fallar en silencio es peor que fallar.

**Cambiar el stub sí es un despliegue manual**, porque es lo único que vive
dentro del trigger. Pasa poquísimo: cambia si se mueve el repositorio, la
rama o la ruta del archivo. Cuando pase, se escribe primero acá y se pega
después.

### Qué versión corrió

La primera línea del prompt declara la versión:

```
VERSIÓN v15 · 2026-08-21 · única copia: ...
```

El prompt obliga a copiarla en el bloque 12 del informe semanal, junto con el
SHA del archivo cuando el conector lo entrega. Ya no sirve para detectar
divergencia —no puede haberla— sino para saber, leyendo el Doc de un lunes
cualquiera, exactamente qué texto produjo ese informe. Al subir un cambio,
sube el número de versión y la fecha de esa primera línea.

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

- **v15 · 2026-08-21** — el prompt deja de tener dos copias. El trigger pasa a
  ser un stub que va a buscarlo acá con el conector de GitHub; se agrega
  `prompts/trigger-stub.md`. Decisión de Cristián.
- v9–v14 · 2026-08-20 — ver `git log`.
- **v8 · 2026-08-20** — primera versión versionada. Corrige cinco valores de
  `Fuerza del vínculo` y `Tipo de vínculo` que el prompt nombraba y que no
  existían en Notion; incorpora la regla de git; obliga a declarar la versión
  en el bloque 12.
- v1–v7 — anteriores al repositorio. No hay historial: vivieron solo dentro
  del trigger. v7 es la que corrió hasta el 20-08-2026.
