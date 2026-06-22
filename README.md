# Sitio web académico en Quarto — guía de uso

Este es un **prototipo** de sitio web personal para un matemático, hecho con
[Quarto](https://quarto.org). Esta guía está pensada para usarse **sin saber
programar**: si sabes escribir en un editor de texto y copiar y pegar, puedes
mantener todo el sitio.

> **Idea central.** Tú escribes en archivos de texto sencillos (con extensión
> `.qmd`), usando un poco de notación —Markdown para el texto y LaTeX para las
> fórmulas— y Quarto los convierte en una página web bonita. No tocas HTML.

---

## Índice

1. [Qué hay en este proyecto](#1-qué-hay-en-este-proyecto)
2. [Instalar Quarto](#2-instalar-quarto)
3. [Ver el sitio en vivo mientras editas](#3-ver-el-sitio-en-vivo-mientras-editas)
4. [Crear una entrada nueva del blog (paso a paso)](#4-crear-una-entrada-nueva-del-blog-paso-a-paso)
5. [Chuleta de matemáticas en LaTeX](#5-chuleta-de-matemáticas-en-latex)
6. [Añadir una publicación nueva](#6-añadir-una-publicación-nueva)
7. [Cambiar título, menú y colores](#7-cambiar-título-menú-y-colores)
8. [Publicar el sitio en internet](#8-publicar-el-sitio-en-internet)

---

## 1. Qué hay en este proyecto

| Archivo / carpeta        | Para qué sirve                                                        |
|--------------------------|-----------------------------------------------------------------------|
| `_quarto.yml`            | El "panel de control": título, menú, tema, colores, macros de LaTeX.  |
| `index.qmd`              | La página de **Inicio** (tu perfil: foto, bio, enlaces).              |
| `publicaciones.qmd`      | La lista de **Publicaciones** (se genera sola desde el `.bib`).        |
| `blog.qmd`               | El **listado** del blog (se genera solo a partir de `posts/`).         |
| `cv.qmd`                 | La página de **CV** con enlace al PDF descargable.                    |
| `posts/`                 | Una carpeta por cada entrada del blog.                                |
| `referencias.bib`        | La base de datos de tus citas bibliográficas.                          |
| `styles.scss` / `styles-dark.scss` | Colores y tipografía (modo claro y oscuro).                 |
| `images/`                | Imágenes del sitio (la foto de perfil, etc.).                          |
| `files/`                 | Archivos para descargar (p. ej. `cv.pdf`).                            |
| `_site/`                 | El sitio web **ya generado**. No se edita a mano; Quarto lo crea.      |

Todo lo que verás marcado como **`[REEMPLAZAR ...]`** es un hueco que debes
rellenar con tus datos reales (tu nombre, tu correo, tus enlaces, etc.).

---

## 2. Instalar Quarto

1. Entra en la página oficial de descargas:
   **<https://quarto.org/docs/get-started/>**
2. Descarga el instalador para tu sistema (Windows, macOS o Linux).
3. Ábrelo y sigue los pasos (Siguiente → Siguiente → Instalar), como cualquier
   otro programa.
4. Para comprobar que quedó bien instalado, abre una **terminal**
   (en Windows: "Símbolo del sistema" o "PowerShell"; en macOS: "Terminal") y
   escribe:

   ```bash
   quarto --version
   ```

   Si te muestra un número de versión (p. ej. `1.9.38`), ¡listo!

> **Recomendado:** instala también [Visual Studio Code](https://code.visualstudio.com/)
> y, dentro de él, la extensión **"Quarto"**. Te da un botón de
> previsualización y resaltado de las fórmulas mientras escribes. No es
> obligatorio, pero hace la vida mucho más fácil.

---

## 3. Ver el sitio en vivo mientras editas

Abre una terminal **dentro de la carpeta del proyecto** (la que contiene este
README) y ejecuta:

```bash
quarto preview
```

Esto abre el sitio en tu navegador. La gracia es que, mientras dejas ese
comando en marcha, **cada vez que guardes un archivo el navegador se actualiza
solo** con tus cambios. Para detenerlo, vuelve a la terminal y pulsa
`Ctrl + C`.

Cuando quieras generar la versión final (la carpeta `_site/`), usa:

```bash
quarto render
```

---

## 4. Crear una entrada nueva del blog (paso a paso)

La forma más fácil es **copiar una entrada que ya existe** y modificarla.

1. Ve a la carpeta `posts/`. Verás carpetas como `bienvenida/`, `teorema/`,
   `citas/`. Cada carpeta es una entrada.
2. **Copia y pega** una de ellas (por ejemplo `bienvenida/`) y renombra la
   copia con el tema de tu nuevo post, p. ej. `posts/mi-primer-post/`.
   - Usa nombres en minúsculas y sin espacios ni acentos (usa guiones):
     `mi-primer-post`, no `Mi Primer Post`.
3. Dentro de tu carpeta nueva, abre el archivo `index.qmd` en un editor de
   texto. Arriba del todo verás el **"front matter"** entre dos líneas de `---`.
   Cámbialo:

   ```yaml
   ---
   title: "El título de mi entrada"
   description: "Una frase corta que resume el post."
   author: "Prof. Tu Nombre"
   date: 2026-06-22          # Fecha en formato AÑO-MES-DÍA.
   categories: [análisis, divulgación]   # Etiquetas; pon las que quieras.
   ---
   ```

4. Debajo del segundo `---`, **borra el contenido de ejemplo y escribe el
   tuyo**. Usa la chuleta de la sección siguiente para las fórmulas.
5. Guarda. Si tienes `quarto preview` en marcha, el post aparecerá solo en el
   blog (ordenado por fecha). **No hace falta tocar `blog.qmd`**: la lista se
   actualiza sola.

> Si tu post lleva una imagen, guárdala **dentro de la carpeta del post** y
> escríbela así: `![Texto descriptivo](mi-imagen.png)`.

---

## 5. Chuleta de matemáticas en LaTeX

Las fórmulas se escriben en **LaTeX**. Hay dos modos:

- **En línea** (dentro de un párrafo): se rodea con un signo de dólar.
  `La función $f(x) = x^2$ es continua.` → La función $f(x)=x^2$ es continua.
- **En bloque** (centrada, en su propia línea): se rodea con dos dólares
  `$$ ... $$`.

### Macros propias (atajos) ya definidas

En `_quarto.yml` hay definidos unos atajos para no escribir tanto. Ya puedes
usarlos en cualquier post:

| Escribes | Sale        | | Escribes      | Sale                |
|----------|-------------|-|---------------|---------------------|
| `\RR`    | ℝ           | | `\abs{x}`     | \|x\| (con tamaño automático) |
| `\ZZ`    | ℤ           | | `\norm{v}`    | ‖v‖                 |
| `\NN`    | ℕ           | | `\set{x}`     | { x }               |
| `\QQ`    | ℚ           | | `\CC`         | ℂ                   |

**Para crear tus propias macros**, abre `_quarto.yml`, busca la sección
`macros:` y añade una línea. Por ejemplo, para que `\eps` produzca `ε`:

```yaml
macros: {
  RR: "{\\mathbb{R}}",
  eps: "{\\varepsilon}"        # <-- tu macro nueva
}
```

(Ojo: dentro de las comillas, las barras `\` de LaTeX van **dobles**: `\\`.)

### Teoremas, lemas y demostraciones

Se escriben con "bloques" de Quarto. El número ("Teorema 1") lo pone Quarto
solo, y puedes referenciarlo después:

```markdown
::: {#thm-miteorema}
## Título del teorema

Aquí va el enunciado, con fórmulas como $a^2 + b^2 = c^2$.
:::

::: {.proof}
Aquí va la demostración. Para cerrarla: $\blacksquare$
:::

Como vimos en el [Teorema @thm-miteorema], ...
```

Etiquetas disponibles: `#thm-` (teorema), `#lem-` (lema), `#cor-` (corolario),
`#prp-` (proposición), `#def-` (definición), y la clase `.proof` (demostración).

### Ecuaciones numeradas y referencias cruzadas

```markdown
$$
e^{i\pi} + 1 = 0
$$ {#eq-euler}

La identidad anterior es la @eq-euler.
```

Quarto numera la ecuación y `@eq-euler` se convierte en "Ecuación 1". Como
alternativa al estilo LaTeX puro, también funciona `\begin{equation}\label{...}`
con `\eqref{...}` (ver el post de ejemplo "Demostración de un teorema").

### Entornos habituales (copiar y pegar)

```latex
$$
\begin{align}                       % varias líneas alineadas y numeradas
  \int_0^\infty e^{-x}\,dx &= 1, \\
  \sum_{n=1}^\infty \frac{1}{n^2} &= \frac{\pi^2}{6}.
\end{align}
$$

$$
f(x) = \begin{cases}                % definición por casos
  1 & \text{si } x > 0, \\
  0 & \text{si } x \le 0.
\end{cases}
$$

$$
\begin{pmatrix} a & b \\ c & d \end{pmatrix}   % matriz entre paréntesis
$$
```

Símbolos frecuentes: `\mathbb{R}` (ℝ), `\mathcal{F}` (caligráfica),
`\mathfrak{A}` (fraktur), `\forall` (∀), `\exists` (∃), `\in` (∈),
`\subseteq` (⊆), `\cup` (∪), `\cap` (∩), `\otimes` (⊗), `\sum`, `\int`,
`\frac{a}{b}`, `\sqrt{x}`, `x^2`, `x_n`.

El post **"Demostración de un teorema"** (en `posts/teorema/`) usa todo esto;
ábrelo para ver ejemplos reales que puedes copiar.

---

## 6. Añadir una publicación nueva

La lista de la página **Publicaciones** se genera sola desde el archivo
`referencias.bib`. Para añadir un trabajo:

1. Abre `referencias.bib`.
2. La forma más cómoda: en **Google Scholar**, **MathSciNet**, **zbMATH** o
   **arXiv**, busca el trabajo y pulsa "Citar → BibTeX". Te dan un bloque de
   texto listo.
3. Pega ese bloque al final de `referencias.bib`. Tiene esta forma:

   ```bibtex
   @article{apellidoAÑO,
     author  = {Apellido, Nombre},
     title   = {Título del artículo},
     journal = {Nombre de la revista},
     year    = {2025},
     doi     = {10.xxxx/xxxxx}
   }
   ```

4. La palabra justo después de `{` (aquí `apellidoAÑO`) es la **clave de cita**.
   Con ella puedes citar el trabajo dentro de cualquier post escribiendo
   `@apellidoAÑO`.
5. Guarda. La publicación aparecerá sola en la página de Publicaciones.

---

## 7. Cambiar título, menú y colores

- **Título del sitio y menú:** abre `_quarto.yml`. Está todo comentado en
  español, sección por sección (título, botones del menú, pie de página).
- **Colores y tipografía:** abre `styles.scss` (modo claro) y, si quieres,
  `styles-dark.scss` (modo oscuro). Cambia el valor de `$primary` por otro
  color y guarda.
- **Tema general:** en `_quarto.yml`, en la línea `theme:`, prueba a cambiar
  `cosmo` por `litera`, `flatly`, `lumen`, etc.
  ([catálogo de temas](https://quarto.org/docs/output-formats/html-themes.html)).

---

## 8. Publicar el sitio en internet

Este prototipo **funciona en local** (en tu ordenador). Cuando decidas
publicarlo, las dos opciones gratuitas más comunes son:

- **GitHub Pages** — gratis, ideal si subes el proyecto a GitHub.
  Guía oficial: <https://quarto.org/docs/publishing/github-pages.html>
- **Netlify** — gratis, muy sencillo arrastrando la carpeta `_site/`.
  Guía oficial: <https://quarto.org/docs/publishing/netlify.html>

En ambos casos, el comando mágico suele ser uno solo (p. ej.
`quarto publish gh-pages`). **Esto lo dejamos para más adelante**: por ahora el
objetivo es que el flujo de escritura te resulte cómodo.

---

¿Dudas? La documentación oficial de Quarto es excelente y está llena de
ejemplos: **<https://quarto.org/docs/guide/>**.
