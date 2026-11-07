# 📘 Guía de Ejercicios — Velocidad Angular y Movimiento Circular

![Licencia](https://img.shields.io/badge/Licencia-GPLv3-blue.svg)
![LaTeX](https://img.shields.io/badge/LaTeX-008080?logo=latex&logoColor=white)
![TikZ](https://img.shields.io/badge/TikZ-PGF-green)
![Física](https://img.shields.io/badge/Mecánica-Clásica-orange)
![dependencias](https://img.shields.io/badge/dependencias-ninguna-success)

Documento académico en LaTeX con fundamentación teórica, ejemplos desarrollados paso a paso y banco de 25 problemas resueltos sobre **velocidad angular y movimiento circular**. Incluye diagramas generados con TikZ/PGFPlots, tabla de soluciones completa y referencias a la literatura clásica (Resnick, Sears, Tipler).

Diseñado como material didáctico para cursos de física de nivel medio superior y superior.

🔗 **Proyecto principal:** [Simulador de Movimiento Circular](../../) — la guía puede usarse como laboratorio virtual complementario al simulador HTML.

## Tabla de contenidos

- [1. Contenido del documento](#1-contenido-del-documento)
- [2. Requisitos](#2-requisitos)
- [3. Compilación local](#3-compilación-local)
- [4. Compilación en Overleaf](#4-compilación-en-overleaf)
- [5. Compilación con Makefile](#5-compilación-con-makefile)
- [6. Estructura de archivos](#6-estructura-de-archivos)
- [7. Paquetes LaTeX requeridos](#7-paquetes-latex-requeridos)
- [8. Personalización](#8-personalización)
- [9. Solución de problemas](#9-solución-de-problemas)
- [10. Contribuir](#10-contribuir)
- [11. Licencia](#11-licencia)

---

## 1. Contenido del documento

| Sección | Descripción |
|---------|-------------|
| **Marco Teórico** | Definición de MCU, velocidad angular ω, relaciones con periodo, frecuencia, velocidad tangencial, aceleración centrípeta, fuerza centrípeta, energía cinética y momento angular. |
| **Diagrama TikZ** | Objeto girando con vectores de **v** (rojo), **a_c** (verde) y **F_c** (azul). |
| **Tabla de relaciones** | Todas las fórmulas clave en función de ω. |
| **3 Ejemplos desarrollados** | Básico (cálculo directo), Intermedio (conversión de unidades), Avanzado (péndulo cónico). |
| **Banco de 25 problemas** | 8 básicos + 9 intermedios + 8 avanzados. |
| **Tabla de soluciones** | `longtable` con las 25 soluciones completas. |
| **Referencias** | Resnick, Sears, Tipler, Hewitt, Khan Academy, HyperPhysics. |

### Temas cubiertos en los ejercicios

- Conversiones rpm ↔ rad/s ↔ Hz
- Cálculo de v, a_c, F_c, E_c, L
- Ruedas conectadas por banda
- Curvas peraltadas y fricción
- Péndulo cónico
- MCU vertical (punto crítico)
- Satélites en órbita
- Centro de masas
- Plataforma giratoria

---

## 2. Requisitos

### Opción A — Compilación local

| Sistema | Distribución recomendada |
|---------|--------------------------|
| **Linux** | TeX Live completo: `sudo apt install texlive-full` (Debian/Ubuntu) o `sudo dnf install texlive-scheme-full` (Fedora) |
| **macOS** | MacTeX: [https://tug.org/mactex/](https://tug.org/mactex/) |
| **Windows** | MiKTeX: [https://miktex.org/](https://miktex.org/) o TeX Live |

### Opción B — Sin instalación

- **Overleaf**: [https://www.overleaf.com](https://www.overleaf.com) (gratis, compilación en la nube)

---

## 3. Compilación local

### Compilación manual

```bash
# 1. Sitúate en la carpeta del proyecto
cd movimientocircular

# 2. Primera pasada (genera el PDF y las referencias internas)
pdflatex VelocidadAngular.tex

# 3. Segunda pasada (resuelve referencias cruzadas y números de página)
pdflatex VelocidadAngular.tex
```

El PDF resultante queda en `VelocidadAngular.pdf`.

### Si usas bibliografía BibTeX

```bash
pdflatex VelocidadAngular.tex   # 1ª pasada
bibtex VelocidadAngular          # procesa bibliografia.bib
pdflatex VelocidadAngular.tex   # 2ª pasada
pdflatex VelocidadAngular.tex   # 3ª pasada
```

### Compilación en un solo comando (recomendado)

```bash
latexmk -pdf -interaction=nonstopmode VelocidadAngular.tex
```

`latexmk` detecta automáticamente cuántas pasadas son necesarias y ejecuta `bibtex` si hace falta.

---

## 4. Compilación en Overleaf

1. Entra en [https://www.overleaf.com](https://www.overleaf.com) y crea un proyecto vacío.
2. Sube los siguientes archivos:
   - `VelocidadAngular.tex` (documento principal)
   - `bibliografia.bib` (referencias)
   - `Makefile` (opcional, Overleaf no lo usa pero sirve como documentación)
3. En **Menu → Settings**, verifica:
   - **Compiler**: `pdfLaTeX`
   - **TeX Live version**: `2023` o superior
4. Pulsa **Recompile**.
5. Descarga el PDF generado con el botón **Download PDF**.

> 💡 **Tip**: si Overleaf no encuentra las referencias, añade al inicio del `.tex`:
> ```latex
> \bibliographystyle{plain}
> \bibliography{bibliografia}
> ```

---

## 5. Compilación con Makefile

Si tienes `make` instalado (Linux, macOS, Git Bash en Windows):

```bash
# Desde la raíz del repositorio
make              # Compila la guía (2 pasadas)
make bib          # Compila con BibTeX (3 pasadas)
make clean        # Borra archivos auxiliares
make distclean    # Borra auxiliares + PDF
make help         # Muestra todos los objetivos
```

### Objetivos disponibles

| Objetivo | Descripción |
|----------|-------------|
| `make` / `make guia` | Compila la guía con 2 pasadas de `pdflatex`. |
| `make bib` | Compila con `bibtex` + 3 pasadas de `pdflatex`. |
| `make guia-docs` | Compila la guía si está en `docs/guia-ejercicios/`. |
| `make clean` | Elimina archivos auxiliares (`.aux`, `.log`, `.out`, etc.). |
| `make distclean` | Elimina auxiliares y el PDF generado. |
| `make serve` | Sirve el simulador HTML en `http://localhost:8000`. |
| `make help` | Muestra la ayuda. |

---

## 6. Estructura de archivos

```
movimientocircular/
├── README.md                       ← README principal del proyecto
├── LICENSE                         ← GNU GPL v3
├── Makefile                        ← compila la guía
├── .gitignore                      ← exclusiones para Git
├── VelocidadAngular.tex            ← documento principal en LaTeX
├── VelocidadAngular.pdf            ← PDF compilado (generado)
├── bibliografia.bib                ← referencias BibTeX
├── simulador.html                  ← versión escritorio
├── simulador-mobile.html           ← versión smartphone
├── simulador-universal.html        ← versión tablet/laptop/TV
└── docs/
    ├── guia-ejercicios/
    │   ├── guia-ejercicios.tex     ← (opcional) copia de la guía
    │   ├── Makefile                ← makefile alternativo
    │   ├── bibliografia.bib        ← (opcional) copia de las refs
    │   └── README.md               ← este archivo
    └── capturas/
        └── .gitkeep                ← placeholder para capturas
```

### Archivos principales

| Archivo | Descripción |
|---------|-------------|
| `VelocidadAngular.tex` | Documento LaTeX completo: marco teórico, ejemplos, banco de problemas, tabla de soluciones y referencias. |
| `bibliografia.bib` | Base de datos BibTeX con las referencias del documento. |
| `Makefile` | Automatiza la compilación del PDF. |

---

## 7. Paquetes LaTeX requeridos

| Paquete | Función |
|---------|---------|
| `amsmath`, `amssymb` | Símbolos y entornos matemáticos |
| `babel-spanish` | Soporte de idioma español |
| `geometry` | Márgenes de página |
| `tikz` + `pgfplots` | Diagramas y gráficas |
| `longtable` | Tabla de soluciones extendida |
| `hyperref` | Enlaces internos y externos |
| `xcolor` | Colores para los diagramas |
| `booktabs` | Tablas profesionales |
| `enumitem` | Listas personalizadas |
| `parskip` | Espaciado entre párrafos |

Todos estos paquetes vienen incluidos en **TeX Live** y **MiKTeX** por defecto. En Overleaf también están disponibles.

### Instalación manual de paquetes (si faltan)

```bash
# Ubuntu/Debian
sudo apt install texlive-latex-extra texlive-pictures texlive-science

# Fedora
sudo dnf install texlive-collection-latexextra texlive-collection-pictures

# macOS (MacTeX)
sudo tlmgr install pgfplots longtable booktabs enumitem parskip

# MiKTeX (Windows)
# Abre MiKTeX Console → Packages → busca el paquete → Install
```

---

## 8. Personalización

### Cambiar los datos del autor

Busca al inicio de `VelocidadAngular.tex` el bloque `\author`:

```latex
\author{MTI. Juan Carlos Santiago Sánchez\\[0.2em]
\texttt{juancarlos.santiago.cb161@dgeti.sems.gob.mx}}
```

Sustituye por tus datos.

### Añadir más ejercicios

Duplica la estructura de un ejercicio existente dentro de las enumeraciones por nivel:

```latex
\begin{enumerate}
  \setcounter{enumi}{25}   % para continuar la numeración
  \item Nuevo problema...
\end{enumerate}
```

No olvides añadir la solución correspondiente a la `longtable` final.

### Cambiar los colores del diagrama

En el diagrama general con TikZ, los colores están así:

```latex
\draw[->, thick, red!70!black, ...]   % velocidad
\draw[->, thick, green!50!black, ...] % aceleración centrípeta
\draw[->, thick, blue!70!black, ...]  % fuerza centrípeta
```

Sustituye los colores por los que prefieras.

### Ajustar márgenes y tamaño de página

Edita la línea de `geometry`:

```latex
\geometry{margin=2.2cm}
```

---

## 9. Solución de problemas

### ❌ Error: `File 'pgfplots.sty' not found`

**Solución:** instala el paquete `pgfplots` (ver sección 7).

### ❌ Error: `Package babel Error: You haven't defined the language spanish`

**Solución:** instala el paquete `babel-spanish`:
```bash
sudo apt install texlive-lang-spanish
```

### ❌ Las referencias aparecen como `[??]`

**Solución:** ejecuta `bibtex` y recompila dos veces más:
```bash
pdflatex VelocidadAngular.tex
bibtex VelocidadAngular
pdflatex VelocidadAngular.tex
pdflatex VelocidadAngular.tex
```

### ❌ Los números de ecuación o figuras están desfasados

**Solución:** borra el archivo `.aux` y recompila:
```bash
rm VelocidadAngular.aux
pdflatex VelocidadAngular.tex
pdflatex VelocidadAngular.tex
```

### ❌ Los diagramas TikZ no se ven

**Solución:** verifica que el paquete `tikz` esté instalado y que la librería `babel` esté cargada **después** de `tikz`:
```latex
\usepackage{tikz}
\usetikzlibrary{babel}   % evita choque con babel-spanish
```

### ❌ Error `! Package pgfplots Error: Could not locate request file`

**Solución:** actualiza `pgfplots` a la versión más reciente. En Overleaf, cambia la versión de TeX Live a 2023 o superior.

---

## 10. Contribuir

Este proyecto es software libre bajo GPL v3 y todas las contribuciones son bienvenidas.

1. Haz fork del repositorio.
2. Crea una rama: `git checkout -b feature/nuevos-ejercicios`.
3. Haz commit: `git commit -m "feat: añade 10 ejercicios de péndulo cónico"`.
4. Haz push: `git push origin feature/nuevos-ejercicios`.
5. Abre un pull request.

### Buenas prácticas

- Compila el documento dos veces antes de hacer commit para asegurar que las referencias cruzadas estén correctas.
- Si añades ejercicios, incluye siempre su solución en la `longtable` final.
- Si añades diagramas, usa el mismo estilo de colores y etiquetas que los existentes.
- Mantén el estilo del código LaTeX (comentarios en español, entornos numerados).
- Al ser GPL v3, tus contribuciones se integrarán bajo la misma licencia.

### Ideas especialmente buscadas

- Ejercicios de aplicación a atracciones de feria (ruedas de la fortuna, centrifugadoras).
- Problemas de transmisión por bandas y engranajes.
- Sección de movimiento circular no uniforme (MCUV).
- Traducción al inglés, francés o portugués.
- Versión interactiva en HTML/JS con GeoGebra o Canvas.

---

## 11. Licencia

**Guía de Ejercicios — Velocidad Angular y Movimiento Circular**

Copyright (C) 2026

Este documento es documentación libre: puedes redistribuirlo y/o modificarlo bajo los términos de la GNU General Public License tal como la publica la Free Software Foundation, ya sea la versión 3 de la Licencia, o (a tu elección) cualquier versión posterior.

|  |  |
|--|--|
| Licencia | GNU General Public License v3.0 |
| SPDX | GPL-3.0-or-later |
| Copyright | (C) 2026 |
| Texto legal completo | [LICENSE](../../LICENSE) · [gnu.org/licenses/gpl-3.0](https://www.gnu.org/licenses/gpl-3.0.txt) |

---

## 📬 Contacto

**MTI. Juan Carlos Santiago Sánchez**

- GitHub: [@jcteacher-lab](https://github.com/jcteacher-lab)
- Correo: juancarlos.santiago.cb161@dgeti.sems.gob.mx

---

> *"La física no es solo fórmulas: es ver el mundo moverse y entender por qué."*

Hecho con ❤️ y con libertad — GPL v3 garantiza que seguirá siendo libre.