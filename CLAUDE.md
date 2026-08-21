# CLAUDE.md — Sistema de registro y monitoreo de Cristián Carrère

Este repositorio versiona **el prompt de la rutina semanal y nada más**. El
sistema que ese prompt ejecuta no es código y no vive acá. Lo primero que
hay que hacer es ir a leerlo.

---

## Regla de trabajo del autor: cero tolerancia a información inventada

Distinguir siempre entre **(a) hecho verificado, (b) inferencia razonada,
(c) especulación**. Si algo no se sabe, se dice. No se rellena un hueco con
algo plausible. Un dato que no consta se deja vacío, y esa ausencia es
información.

Tres corolarios que ya costaron caro:

- **Nunca sobrescribas texto de Cristián.** Si un campo ya tiene texto
  suyo, se anexa con fecha; el reemplazo solo es legítimo en un dato que
  efectivamente caducó.
- **En Notion no se puede borrar una fila.** Un duplicado queda para
  siempre. Antes de crear cualquier ficha se busca por variantes; ante la
  duda, no se crea.
- **No se crean filas cuyo contenido haya que inventar.** Hay ~849 personas
  sin organización enlazada precisamente por esto: enlazarlas exigiría
  inventar unas 400 organizaciones desde el dominio del correo.

---

## Dónde vive el sistema

**La fuente es la Política de Registro, en Notion.** Fija el propósito, el
alcance, los principios, los objetos, el ciclo de siete fases con sus puntos
de control, las reglas de acreditación y la gobernanza. **Léela entera antes
de ejecutar nada; no la reproduzcas acá.**

| qué | dónde |
|---|---|
| **Política de Registro** | Notion `3c38ae9c-ac0a-8145-a2e1-f0d95d6978c7` |
| Sistema de Registro *(antecesora, a archivar cuando la Política se valide)* | Notion `3c18ae9c-ac0a-8173-bae8-e4869b37efc7` |
| Protocolo de archivos y carpetas | Notion `3c18ae9c-ac0a-81ea-b30e-ef35516d15e7` |
| Carta de Navegación — **SOLO LECTURA, ni una coma** | Drive `1ZrYE8gs46qEECnBuU_846IGSbyTS0xLGo5xhzVa0irk` |

**Las seis bases de Notion**, que son todo el registro:

```
Personas                    908e2c78-d776-4109-8cda-483d323e9dc2
Organizaciones              bedf6bf2-ab91-4442-911c-781c579cdd77
Portafolio de Proyectos     cedd1769-9ef6-463f-833d-ad1bfd196df9
Oportunidades de contrato   a5fe518e-c88c-4216-818e-803c5cbdf2bb
Competencias                e3489a68-fccb-43f8-94a7-ecb50f05baa2
Evidencia                   afa5e99c-6969-4e63-9087-68ebbfed5945
```

**Drive:**

```
5. Control y Registro ······················ 0AAqxYsCL91CvUk9PVA
  └ 3. Registro de Proyectos ··············· 1OV7mTP5-Z66j2d_w2hxGL3OlwujRT6aw
      ├ Entregables ························ 15bmrns7pj9iBdSr6Tu2YMLLLMLouFV91
      └ Medios de verificación ············· 1EQ_h0EW8bvn6IaT9yocjkzogvo_n_cEe
          ├ Proyectos ······················ 1FzFoZS2WkFDTc1VABoBdfefdLC8pR62l
          └ Cargos ························· 1pz_heA-5Ny1epc-VnqFaqPpX3gEOBE0L
  └ 5. Monitoreo semanal ··················· 1wGSIrAOsOMcMu3XN6hluWFIRQgWpCDLf
Operaciones ································ 0AN7vMH3UzJ2VUk9PVA
Oportunidades ······························ 0AFHp3oDtigKLUk9PVA
  ├ Actuales ······························· 16RnAdkRZ7UogHbSQF0rCU3pHQFzGR4qB
  ├ Sin Concretar ·························· 1NtBSla9r21DM2EmXreIDSHa3Owz8O3kt
  └ Fondos ································· 14EZFp-nsTjLczL57kx4OwUeZ0ZE9wnNf
```

**Los nombres de carpeta cambian; los identificadores no.** Si un id no
resuelve, buscar por título antes de darlo por perdido, y **no inventar
ubicaciones**.

**Lo que NO está acá y no debe copiarse acá.** El sistema no es código.
Duplicarlo en el repositorio crearía exactamente el problema que la regla de
git existe para evitar: dos copias que se separan en silencio. Ya pasó una
vez, con una página de reglas paralela que seguía mandando clasificar
personas en tres bases semanas después de que esas tres bases se fundieran
en una.

---

## El prompt de la rutina semanal

```
prompts/
  monitoreo-semanal.md   ← el prompt de la Routine, ~56 KB
  trigger-stub.md        ← su reemplazo futuro, aún no desplegable
```

**Fuente canónica: `prompts/monitoreo-semanal.md`.** La copia que corre vive
dentro del trigger `trig_01RTagcd3J82T42seo9C4Kp7`, cron `0 12 * * 1`.

**LA REGLA: todo cambio se escribe primero acá, se commitea, y recién
entonces se despliega al trigger. Nunca al revés, y nunca solo en uno de los
dos.** Un cambio hecho solo en el trigger no deja rastro; uno hecho solo acá
no corre. La primera línea del archivo declara la versión y el informe
semanal la copia, así que basta comparar el Doc del lunes con el último
commit para ver si las dos copias se separaron.

**Cómo se despliega:** `update_trigger` con el contenido completo del
archivo, y después **verificar por SHA256** contra el archivo local leyendo
la respuesta guardada. No basta con que la llamada no falle.

**Por qué hay dos copias y no una.** El diseño correcto sería que el trigger
no contuviera instrucciones sino la orden de venir a leer este archivo con
el conector de GitHub. Está escrito, en `trigger-stub.md`. **No se puede
desplegar, y está medido:** ver abajo.

---

## Hechos del entorno, todos verificados

**La sesión que abre el trigger no tiene el conector de GitHub.** Medido el
21-08-2026 disparando el propio trigger semanal con un prompt de prueba. Los
servidores presentes son Gmail, Notion, Google Drive, Google Calendar,
Spotify, Undermind y claude-code-remote; `get_file_contents` no está. Un
trigger creado o editado por herramienta solo hereda los conectores que
tenga la sesión que lo edita. **Lo desbloquea habilitar GitHub en los
conectores de la Routine, desde la interfaz de Routines de claude.ai** — y
después repetir la prueba antes de pegar el stub.

**La rutina no debe usar WebFetch.** Pide autorización caso a caso y deja la
corrida colgada esperando una aprobación que nadie va a dar: el 19-08-2026
la sesión quedó con ocho solicitudes en cola y no produjo nada.

### Trampas de la API de Notion

Todas encontradas ejecutando, no leídas en la documentación:

- **`ALTER COLUMN … SET SELECT(...)` borra la descripción de la columna** si
  no se vuelve a suministrar el `COMMENT`. Convertir el tipo de una columna
  la borra igual. **Copiarla antes.**
- **`COMMENT` se ignora en silencio en columnas de tipo RELATION.** No hay
  forma de escribir la glosa por API; hay que pegarla a mano.
- **`DROP COLUMN "X"; RENAME COLUMN "Y" TO "X"` en un mismo lote produce
  `"X 1"`.** Hace falta un segundo `RENAME`.
- **`update_content` devuelve éxito y no hace nada** cuando el `old_str` no
  calza exactamente. **Verificar después de cada lote**, releyendo la página
  y buscando el texto nuevo.
- **Un `page_id` inventado se acepta y queda como relación colgante**, sin
  error. Comprobar los destinos.
- Una data source **sí** se puede mandar a la papelera, con `in_trash: true`.
- Las relaciones se pueblan **desde cualquiera de los dos lados**: escribir
  la propiedad dual en una fila es mucho más barato que N actualizaciones.
- **El texto comentado arrastra marcado invisible** `<span
  discussion-urls="…">` en el markdown almacenado. Editarlo exige incluir
  ese marcado y deja el comentario huérfano: **editar alrededor.**

### Herramientas que devuelven más de lo que cabe

`list_triggers` y `notion-fetch` sobre páginas grandes exceden el límite y
se guardan en un archivo. No hay que reintentar: se leen con `python3`
troceando por rangos de caracteres, o parseando el JSON y sacando solo el
campo que interesa.

### Qué falta en el contenedor

No hay `pdftotext`, `pdftoppm` ni `soffice` funcional, y `pypdf` está roto.
Para leer un PDF: extractor propio con `zlib` sobre los flujos
`FlateDecode`, filtrando a los que contienen `BT` + `Tf` + `Tj`/`TJ`. Un PDF
cifrado con RC4 no se lee así, y en ese caso **se dice que no se pudo leer**
en vez de suponer su contenido.

---

## Estado y pendientes

**El plan de implementación vive en la sección 8 de la Política**, no acá.
Son trece actividades; las tres primeras dejan un propósito a medias
—dónde se registra la calidad de la ejecución, describir Relacionamiento,
diseñar la comunicación de cierre— y las otras diez son trabajo acotado.

Lo que es propio de este repositorio:

- **Desplegar el stub** cuando GitHub esté habilitado en la Routine, después
  de repetir la prueba.
- **Actualizar el §4 del prompt** para que apunte a la Política
  `3c38ae9c-ac0a-8145-a2e1-f0d95d6978c7` cuando Cristián valide la página
  nueva y archive el Sistema de Registro. Hoy apunta a la vieja.

## Historial del prompt

- **v16 · 21-08-2026** — deja escrito que la sesión del trigger no tiene el
  conector de GitHub, medido ese día sobre el propio trigger.
- v15 · 21-08-2026 — daba por hecho lo contrario. **Nunca se desplegó.**
- v8–v14 · 20-08-2026 — ver `git log`.
- v1–v7 — anteriores al repositorio. No hay historial: vivieron solo dentro
  del trigger.
