STUB DEL TRIGGER · v1 · 2026-08-21 · NO DESPLEGADO
Este archivo es el texto que iría dentro del trigger `trig_01RTagcd3J82T42seo9C4Kp7`,
en reemplazo del prompt completo. **Hoy no se puede usar.**

Medido el 21-08-2026, disparando ese mismo trigger con un prompt de prueba: la sesión
que abre la tarea programada NO tiene el conector de GitHub. Los servidores presentes
son Gmail, Notion, Google Drive, Google Calendar, Spotify, Undermind y
claude-code-remote; `get_file_contents` no está entre las herramientas. Un stub que
mandara a leer el repositorio no podría leerlo.

Qué lo desbloquea: habilitar GitHub en los conectores de la Routine, desde la interfaz
de Routines de claude.ai. Después se repite la prueba y, si da SÍ, se pega lo de abajo.

El prompt sigue siendo `prompts/monitoreo-semanal.md`, en este mismo repositorio.
Lo de abajo, entre las marcas, es lo que se pegaría en el trigger tal cual.

---8<--- COPIAR DESDE ACÁ ---8<---

Ejecuta el MONITOREO SEMANAL de Cristián Carrère (cristian@espaciotp.cl).

Las instrucciones no están acá. Están en GitHub, y son lo primero que tienes que ir a buscar. Este mensaje no es un resumen del prompt ni una versión corta: es solo la orden de ir a leerlo y qué hacer si no lo conseguiste.

1 · LEE EL PROMPT

Con el conector de GitHub —la herramienta `get_file_contents` del servidor de GitHub, NO WebFetch—:

    repositorio  CristianCarrereAlvarez/monitoreo_y_control
    rama         main
    archivo      prompts/monitoreo-semanal.md

Ese archivo es el prompt completo, unos 56 KB. Léelo entero antes de ejecutar nada y síguelo tal como está escrito. Su primera línea declara la VERSIÓN; el prompt te va a pedir que la copies en el bloque 12 del informe. Si la respuesta de la herramienta trae además el SHA del archivo, anótalo ahí también: es lo que permite saber después exactamente qué texto corrió.

2 · SI NO PUDISTE LEERLO

El conector no está disponible, el repositorio no responde, el archivo no está en esa ruta, o volvió vacío.

NO ejecutes el monitoreo. No lo reconstruyas de memoria, no improvises una versión corta, no hagas «lo que se pueda». Ese prompt son reglas que existen porque cada una arregló un error real, y una corrida sin ellas produce un informe que parece correcto y no lo es.

Haz una sola cosa, y termina:

> Envía un correo a cristian@espaciotp.cl con asunto
> «Monitoreo Semanal · [fecha] · NO CORRIÓ: no se pudo leer el prompt»
> y en el cuerpo: qué herramienta intentaste, con qué parámetros, y el error exacto que devolvió.

No crees el Documento, ni el evento de calendario, ni escribas nada en Notion.

Una tarea programada que se cuelga en silencio es peor que una que no corre. Este bloque existe para que el lunes se sepa lo mismo si corrió que si no.

---8<--- HASTA ACÁ ---8<---
