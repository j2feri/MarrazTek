# Guía para actualizar MarrazTek

Estrategia y convenciones para mantener el sitio web de MarrazTek
(`https://j2feri.github.io/MarrazTek/`) vivo y actualizado con apuntes,
ejercicios, vídeos y recursos.

---

## Índice

1. [Principio básico](#1-principio-básico)
2. [Estructura de carpetas](#2-estructura-de-carpetas)
3. [Plantilla de página](#3-plantilla-de-página)
4. [Rutina de actualización](#4-rutina-de-actualización)
5. [Vídeos de YouTube](#5-vídeos-de-youtube)
6. [Convenciones](#6-convenciones)
7. [Qué NO hacer](#7-qué-no-hacer)
8. [Plan semana a semana](#8-plan-semana-a-semana)
9. [Cómo añadir una página nueva](#9-cómo-añadir-una-página-nueva)
10. [Cómo publicar cambios](#10-cómo-publicar-cambios)
11. [Solución de problemas](#11-solución-de-problemas)

---

## 1. Principio básico

> **Una carpeta por asignatura, una página por tema, la misma plantilla
> de 4 secciones siempre, actualizada a medida que enseñas.**

El sitio funciona con HTML y CSS escritos a mano, alojados en GitHub Pages.
No hay Jekyll, ni workflow, ni build step. Cada push a `main` publica los
cambios en ~30 segundos.

**Ventajas de este enfoque:**

- Baja fricción: sin herramientas de build, sin plugins
- Escalable: 100 páginas funcionan igual que 5
- Predecible: el alumnado siempre sabe dónde está cada cosa
- Duradero: el sitio sobrevive años de pequeños cambios

---

## 2. Estructura de carpetas

```
MarrazTek/
├── index.html                    ← portada con navegación
├── style.css                     ← estilos compartidos
├── GUIA.md                       ← este documento
├── MT1/
│   ├── index.html                ← portada de MT1
│   ├── tema1-trazados.html
│   ├── tema2-poligonos.html
│   ├── ejercicios/
│   │   ├── lamina01.pdf
│   │   └── lamina02.pdf
│   └── img/
│       └── tema1-fig01.png
├── MT2/
│   ├── index.html
│   ├── diedrico/
│   │   ├── index.html
│   │   ├── punto-recta-plano.html
│   │   └── intersecciones.html
│   └── pau.html
├── DBH3/
│   └── index.html
└── recursos/
    ├── videos.html               ← lista curada de YouTube
    └── enlaces.html
```

**URLs resultantes:**

- `https://j2feri.github.io/MarrazTek/MT1/` → portada de MT1
- `https://j2feri.github.io/MarrazTek/MT1/tema1-trazados.html` → tema concreto

**Aviso sobre rutas:** al mover un archivo a una subcarpeta, el enlace al CSS
cambia. Desde `MT1/tema1-trazados.html`, el enlace al CSS es `../style.css`
(subir un nivel).

---

## 3. Plantilla de página

Usa **siempre la misma plantilla** para cada tema. Así crear contenido nuevo
es mecánico y rápido.

```html
<!DOCTYPE html>
<html lang="eu">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tema 1 · Trazados | MT1 | MarrazTek</title>
  <link rel="stylesheet" href="../../style.css">
</head>
<body>

  <header>
    <h1><a href="../../index.html">MarrazTek</a></h1>
    <p>Marrazketa Teknikoa Batxilergoan</p>
  </header>

  <nav class="breadcrumb">
    <a href="../../index.html">Inicio</a> ›
    <a href="../index.html">MT1</a> ›
    <span>Tema 1</span>
  </nav>

  <main>
    <h1>Tema 1 · Trazados fundamentales</h1>

    <!-- 1. TEORÍA -->
    <section>
      <h2>1. Teoría</h2>
      <p>Explicación breve del concepto...</p>
    </section>

    <!-- 2. VÍDEOS -->
    <section>
      <h2>2. Vídeos</h2>
      <ul>
        <li>
          <a href="https://www.youtube.com/watch?v=XXXX" target="_blank" rel="noopener">
            Mediatriz y bisectriz — Canal X
          </a>
          <span class="meta">(5:32)</span>
        </li>
      </ul>
    </section>

    <!-- 3. EJERCICIOS -->
    <section>
      <h2>3. Ejercicios</h2>
      <ul>
        <li><a href="ejercicios/lamina01.pdf">Lámina 1 (PDF)</a></li>
        <li><a href="ejercicios/lamina02.pdf">Lámina 2 (PDF)</a></li>
      </ul>
    </section>

    <!-- 4. RECURSOS EXTRA -->
    <section>
      <h2>4. Recursos</h2>
      <ul>
        <li><a href="#">Mongge — ejercicios interactivos</a></li>
      </ul>
    </section>
  </main>

  <footer>
    <p>MarrazTek · Publicado en GitHub Pages</p>
  </footer>

</body>
</html>
```

Guarda esta plantilla como `plantilla.html` en la raíz del repositorio.
No la enlaces desde ningún sitio — sirve solo para copiar y pegar.

**Las 4 secciones son siempre las mismas:** Teoría / Vídeos / Ejercicios / Recursos.

---

## 4. Rutina de actualización

No intentes construirlo todo de golpe. Elige un ritmo realista:

| Frecuencia | Tarea | Tiempo |
| :--- | :--- | :--- |
| **Semanal** | Añadir el tema de esta semana: teoría + 2–3 vídeos + 1 lámina | 20 min |
| **Mensual** | Actualizar la página de recursos con enlaces nuevos | 10 min |
| **Por trimestre** | Revisar y reorganizar — mover contenido obsoleto | 1 h |
| **Anual** | Archivar materiales PAU del año pasado, refrescar enlaces | 30 min |

**Clave:** actualiza **a medida que enseñas**, no en grandes bloques al final.
El alumnado recibe valor inmediato y tú nunca acumulas 6 horas de trabajo.

---

## 5. Vídeos de YouTube

No incrustes `<iframe>` de YouTube por todas partes. Ralentizan la página y
se rompen cuando los vídeos se eliminan.

**Mejor: enlaza con contexto.**

```html
<li>
  <a href="https://www.youtube.com/watch?v=abc123" target="_blank" rel="noopener">
    Cómo trazar la mediatriz — Profesor X
  </a>
  <span class="meta">5:32 · Español</span>
</li>
```

**Por qué:**

- `target="_blank"` abre en una pestaña nueva — el alumnado no pierde tu página
- `rel="noopener"` evita un problema de seguridad (buena práctica)
- La descripción indica *qué* muestra el vídeo *antes* de hacer clic
- Si el vídeo desaparece, solo hay que borrar el `<li>`

**Cura, no acumules.** Una página con 5 vídeos bien elegidos vale más que
otra con 40 aleatorios.

---

## 6. Convenciones

Establece una pequeña guía de estilo para ti mismo:

| Elemento | Convención |
| :--- | :--- |
| Nombres de archivo | minúsculas, sin espacios, guiones (`tema1-trazados.html`) |
| URLs | iguales que los nombres de archivo |
| Encabezados | `<h2>` para temas principales, `<h3>` para subtemas |
| PDFs | `lamina01.pdf`, `lamina02.pdf` — predecibles |
| Imágenes | `img/tema1-fig01.png` — nunca `IMG_2938.png` |
| Vídeos | incluir siempre duración e idioma |

Estas pequeñas convenciones te ahorran horas después.

---

## 7. Qué NO hacer

- **No montes un CMS.** Ni WordPress, ni Jekyll, ni build step. Elegiste HTML
  puro — sigue con él.
- **No pegues iframes de YouTube por todas partes.** Enlaza con contexto.
- **No crees 20 páginas vacías "para después".** Crea páginas a medida que
  las rellenas.
- **No dupliques el header/footer a mano en 50 páginas.** Si te ves haciéndolo,
  ese es el momento de introducir un pequeño paso de build o un include en JS.

---

## 8. Plan semana a semana

**Semana 1 — Reestructurar**

- Mover los archivos actuales a carpetas por asignatura (`MT1/`, `MT2/`, `DBH3/`)
- Añadir `index.html` dentro de cada carpeta
- Actualizar los enlaces en el `index.html` principal
- Hacer commit y verificar

**Semana 2 — Plantillas**

- Añadir `plantilla.html` en la raíz con el esqueleto de 4 secciones
- No enlazarla desde ningún sitio — es solo para copiar

**Semana 3 en adelante — Contenido**

- Después de cada clase, crear una página de tema desde la plantilla
- Pegar: teoría breve, 2 vídeos, 1 lámina
- Hacer commit

**Fin de trimestre — Limpieza**

- Revisar enlaces rotos
- Mover contenido antiguo a una página "archivo" si hace falta
- Actualizar la lista de la portada

---

## 9. Cómo añadir una página nueva

1. Abre `plantilla.html` y copia todo el contenido.
2. Crea un archivo nuevo en la carpeta correspondiente, con nombre en
   minúsculas y guiones (ej. `tema3-tangencias.html`).
3. Pega el contenido.
4. Cambia:
   - El `<title>`
   - El `href` del CSS (`../style.css` o `../../style.css` según la profundidad)
   - El breadcrumb (las 3 migas de pan)
   - El `<h1>`
   - El contenido de las 4 secciones
5. Enlaza la página nueva desde el `index.html` de la carpeta (y desde el
   principal si es un tema destacado).
6. Commit → push → en ~30 segundos está publicado.

---

## 10. Cómo publicar cambios

**Opción A — Desde la web de GitHub (rápida, para cambios pequeños):**

1. Abre el archivo en GitHub.
2. Haz clic en el lápiz ✏️ (arriba a la derecha del archivo).
3. Edita el contenido.
4. Abajo, en "Commit changes", escribe un mensaje breve.
5. Clic en "Commit changes".
6. Espera ~30 segundos y recarga el sitio con `Ctrl+Shift+R`.

**Opción B — Desde tu ordenador (para cambios grandes):**

```bash
git clone https://github.com/j2feri/MarrazTek.git
cd MarrazTek
# edita los archivos con tu editor (VS Code, etc.)
git add .
git commit -m "Añadir tema 3 de MT1"
git push origin main
```

**Añadir archivos nuevos desde la web:**

- Botón **Add file → Upload files** para PDFs, imágenes, etc.
- Botón **Add file → Create new file** para HTML nuevos.

---

## 11. Solución de problemas

| Síntoma | Causa probable | Solución |
| :--- | :--- | :--- |
| Página en blanco | Archivo HTML vacío | Abrir el archivo en GitHub, comprobar que tiene contenido |
| 404 en una página | Nombre con mayúsculas/minúsculas distintas (`MT1.html` ≠ `mt1.html`) | GitHub Pages es sensible a mayúsculas. Corregir el enlace o el nombre |
| Sin estilos | `style.css` mal enlazado | Comprobar la ruta relativa (`../style.css` según profundidad) |
| Cambios no aparecen | Caché del navegador | Recarga forzada: `Ctrl+Shift+R` |
| Sitio entero da 404 | Pages desactivado o rama incorrecta | Settings → Pages → Source: `Deploy from a branch` · `main` · `/ (root)` |
| Imagen no carga | Ruta mal escrita | Comprobar mayúsculas y que el archivo esté subido en la carpeta correcta |

**Comprobación rápida:** abre la URL directa del archivo, por ejemplo
`https://j2feri.github.io/MarrazTek/style.css`. Si muestra el CSS, el archivo
está bien servido. Si da 404, el problema es la ruta.

---

## Referencias rápidas

**Sintaxis HTML esencial:**

```html
<!-- Comentario -->
<a href="url">texto del enlace</a>
<img src="ruta.png" alt="descripción">
<ul><li>elemento de lista</li></ul>
<h1>Título principal</h1>
<h2>Sección</h2>
```

**Rutas relativas:**

| Desde | Al CSS raíz | A otra página en la misma carpeta |
| :--- | :--- | :--- |
| Raíz (`index.html`) | `style.css` | `MT1.html` |
| Un nivel (`MT1/index.html`) | `../style.css` | `tema1.html` |
| Dos niveles (`MT1/diedrico/index.html`) | `../../style.css` | `punto-recta-plano.html` |

---

*Última actualización: 2026-09-17*
