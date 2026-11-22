# Complacencia de la IA: una demostración

Demostración visual y mínima de la **complacencia** (*sycophancy*) de los modelos de lenguaje: la tendencia de una IA a darle la razón al usuario, elogiarlo y acomodar su respuesta a lo que este parece querer oír, a costa de la exactitud.

Fue presentada en las **V Jornadas de Teoría e Historia de la Historiografía** como apoyo de la ponencia de Albert Mestre.

> **Importante:** las respuestas están **escritas de antemano**. No se conecta con ningún modelo real. La demo es ilustrativa: reconstruye un patrón descrito en la bibliografía para hacerlo visible, no registra la respuesta de un modelo en particular.

## Qué muestra

- Un **prompt fijo**, visible para el público:
  > ¿Cuáles fueron las implicancias de Karl Popper en el campo historiográfico e historiológico con su libro "La miseria del historicismo"?
- Una **respuesta breve** (máximo 300 caracteres).
- Una **barra vertical del 1 al 5**: cuánto "trabajó" el usuario en una sesión hipotética. A mayor nivel, el usuario ya expresó su propia tesis e insiste en ella, y la respuesta se vuelve más complaciente.

Al pasar de un nivel a otro, la demo señala las frases que cambiaron:

| Color | Tipo | Qué indica |
|---|---|---|
| Amarillo | **Se desvía** | Elogios y adopción del encuadre del usuario: el foco pasa del contenido a quien pregunta. |
| Naranja | **Se tuerce** | El contenido contradice o deforma la fuente. |
| Violeta | **Pierde verificabilidad** | Afirmaciones sin cita, generalizaciones o "demostraciones" que no se pueden contrastar. |

Cada frase señalada queda numerada y unida a una nota que explica qué cambió respecto del nivel anterior. Las notas con **∅** indican lo que la respuesta **omitió**: fechas, referencias o conceptos que permitían verificarla. La barra de cada línea y el porcentaje de "texto señalado" se calculan a partir de las frases marcadas.

> Los recuadros y las barras son **señalamientos editoriales** hechos a mano a partir de la fuente, **no la atención del modelo**. La demo lo aclara en pantalla para que no se confunda con una visualización del funcionamiento interno de la IA.

## Cómo usarla

No requiere instalación, servidor ni conexión a internet: es un único archivo HTML.

1. Descargá o cloná este repositorio.
2. Abrí `index.html` con cualquier navegador moderno (Chrome, Edge o Firefox).

Controles:

| Tecla | Acción |
|---|---|
| `↑` `↓` (o `→` `←`) | Subir o bajar de nivel |
| `1` – `5` | Ir directo a un nivel |
| `M` | Ocultar o mostrar los señalamientos |

También se puede usar el mouse sobre la barra o sobre los números.

## Cómo adaptarla a otro tema

Todo el contenido está al principio del `<script>` de `index.html`, en el bloque marcado como `TEXTOS EDITABLES`:

```js
const PROMPT = '¿Tu pregunta?';

const LEVELS = [
  { ctx: 'Primer mensaje · sin contexto previo',
    text: 'Respuesta de referencia, sin marcas.',
    base: 'Por qué esta respuesta sirve de referencia.',
    notes: [] },

  { ctx: '1 h · el usuario dijo: «...»',
    text: '[d]¡Excelente pregunta![/d] Texto con [t]una afirmación torcida[/t] y [v]una sin fuente[/v].',
    notes: [
      { t: 'd', n: 'Nota para el fragmento 1.' },
      { t: 't', n: 'Nota para el fragmento 2.' },
      { t: 'v', n: 'Nota para el fragmento 3.' },
      { t: 'v', n: 'una referencia que la respuesta dejó de mencionar.' }  // sin fragmento: se muestra como "Omite ..."
    ] },
  // ... hasta 5 niveles
];
```

- `ctx`: lo que el usuario hipotético dijo o hizo antes de esa respuesta. Se muestra bajo la barra.
- `text`: la respuesta. Los fragmentos se marcan con `[d]…[/d]` (se desvía), `[t]…[/t]` (se tuerce) y `[v]…[/v]` (pierde verificabilidad).
- `notes`: una nota por fragmento, **en el mismo orden** en que aparecen en el texto. Las notas que sobran al final se muestran como omisiones (∅).
- `WRAP`: cantidad de caracteres por línea (56 por defecto).

Conviene que la respuesta del nivel 1 sea la más fiel a la fuente y no tenga marcas: es la línea de base contra la que se comparan las demás.

## Publicarla en línea (opcional)

Con **GitHub Pages**: en el repositorio, *Settings → Pages → Source: Deploy from a branch*, elegí la rama `main` y la carpeta `/ (root)`. En uno o dos minutos la demo queda disponible en `https://<usuario>.github.io/<repositorio>/`.

## Fuentes

- **Contenido histórico:** Mestre, A. (2021). *Informe sobre "La miseria del historicismo" de Karl Popper*. Informe de pasaje de curso, Seminario de los modelos epistémicos en la reflexión historiológica contemporánea (siglos XIX–XXI). Los errores de los niveles 4 y 5 son los que ese informe refuta en Cardoso, C. F. S. (2000). *Introducción al trabajo de la investigación histórica*. Barcelona: Crítica, p. 110.
- **Marco sobre complacencia y verosimilitud:**
  - Ye, Ibrahim y Bo. *What counts as AI sycophancy? A taxonomy and expert survey of a fragmented construct.*
  - Hagar, Agustianto y Diakopoulos. *Not wrong, but untrue: LLM overconfidence in document-based queries.*
- **Inspiración visual:** la estética del inspector (recuadros, corchetes y barras por línea) se inspira en el "focus monitor" de Sun, C. (2026). *Spaceship IDE: Steer Your Ideas in Realtime, Space Pilot Style*. GitHub. https://github.com/chuanqisun/spaceship

## Licencia

[MIT](LICENSE): podés usarla, modificarla y redistribuirla citando la autoría original.
