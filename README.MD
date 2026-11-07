# Simulador de Movimiento Circular

![Licencia](https://img.shields.io/badge/Licencia-GPLv3-blue.svg)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)
![Responsive](https://img.shields.io/badge/Responsive-✓-success)
![dependencias](https://img.shields.io/badge/dependencias-ninguna-success)

Simulador interactivo de movimiento circular uniforme en HTML, CSS y JavaScript puros. Renderiza en tiempo real un objeto atado a una cuerda que gira alrededor de un pivote, mostrando los vectores de velocidad tangencial, fuerza centrípeta y aceleración centrípeta. Dispone de tres versiones adaptadas a distintos dispositivos (escritorio, móvil y universal para tablet/laptop/TV) con panel de resultados físicos en tiempo real y control total de los parámetros del sistema.

Diseñado como laboratorio virtual para la enseñanza de la mecánica clásica: permite variar la longitud de la cuerda, la velocidad angular y la masa del objeto, observando instantáneamente cómo cambian todas las magnitudes físicas del fenómeno.

Incluye una guía de ejercicios académica en LaTeX que usa el simulador como laboratorio virtual para aplicar las leyes del movimiento circular y la dinámica rotacional.

## Tabla de contenidos

- [1. Características](#1-características)
- [2. Instalación y ejecución](#2-instalación-y-ejecución)
- [3. Estructura del repositorio](#3-estructura-del-repositorio)
- [4. Controles](#4-controles)
- [5. Arquitectura del código](#5-arquitectura-del-código)
- [6. Modelo físico](#6-modelo-físico)
- [7. Personalización](#7-personalización)
- [8. Documentación académica](#8-documentación-académica)
- [9. Roadmap](#9-roadmap)
- [10. Limitaciones conocidas](#10-limitaciones-conocidas)
- [11. Contribuir](#11-contribuir)
- [12. Referencias](#12-referencias)
- [13. Autor](#13-autor)
- [14. Licencia](#14-licencia)
- [15. Agradecimientos](#15-agradecimientos)
- [16. Proyectos relacionados](#16-proyectos-relacionados)

---

## 1. Características

### Visualización en tiempo real
- Objeto circular unido por una cuerda a un pivote central que gira con movimiento circular uniforme.
- **Vectores dinámicos** dibujados sobre el objeto:
  - 🔴 Velocidad tangencial (**v**) — perpendicular al radio.
  - 🟢 Fuerza centrípeta / Tensión (**Fc**) — dirigida al centro.
  - 🟡 Aceleración centrípeta (**ac**) — misma dirección que Fc.
  - 🟣 Trayectoria circular punteada que indica la órbita.
- **Estela luminosa** que muestra las últimas posiciones del objeto.
- **HUD flotante** con las magnitudes clave en pantalla.

### Controles interactivos
- 🔗 **Longitud de la cuerda (r)**: de 0.5 a 3 m.
- 🔄 **Velocidad angular (ω)**: de 0.5 a 10 rad/s.
- ⚖️ **Masa del objeto (m)**: de 0.1 a 10 kg.
- ⏩ **Velocidad de simulación**: de 0.1× a 3×.
- ⏸️ **Pausar / Reanudar** y 🔄 **Reiniciar** el movimiento.

### Resultados físicos calculados en tiempo real
- Velocidad tangencial: `v = ω·r`
- Aceleración centrípeta: `ac = ω²·r`
- Fuerza centrípeta / Tensión: `Fc = m·ac`
- Período: `T = 2π/ω`
- Frecuencia: `f = 1/T` (Hz y RPM)
- Energía cinética: `Ec = ½mv²`
- Momento angular: `L = m·v·r`

### Funciones avanzadas (versión universal)
- **Modo TV / Presentación**: oculta paneles y muestra solo la simulación a pantalla completa.
- **Pantalla completa** mediante Fullscreen API.
- **Atajos de teclado**: `Espacio` (pausa), `R` (reiniciar), `F` (modo TV), `↑/↓` (ω), `←/→` (r).
- **Soporte HiDPI / Retina / 4K** con `devicePixelRatio`.
- **Layout fluido** con `clamp()` y media queries para pantallas desde 320 px hasta 4K.

### Sin dependencias
- HTML + CSS + JavaScript puros.
- No requiere servidor web, frameworks ni conexión a internet.

---

## 2. Instalación y ejecución

### Opción 1 — Abrir directamente
1. Descarga o copia el contenido del simulador deseado en un archivo:
   - `index.html`
2. Haz doble clic en el archivo para abrirlo en cualquier navegador moderno (Chrome, Firefox, Edge, Safari).
3. Listo. No requiere servidor web ni conexión a internet.

### Opción 2 — Servir localmente
```bash
git clone https://github.com/jcteacher-lab/velocidadangular.git
cd velocidadangular
python3 -m http.server 8000
# Luego abre en tu navegador:
http://localhost:8000
```

### Opción 3 — Publicar en GitHub Pages
Sube los archivos a un repositorio público y activa GitHub Pages en la rama `main`. El simulador quedará disponible en:
```
https://jcteacher-lab.github.io/movimientocircular/velocidadangular.html
```

---

## 3. Estructura del repositorio

```
movimientocircular/
├── README.md                       ← este archivo
├── LICENSE                         ← texto legal GNU GPL v3
├── Makefile                        ← compila todo (simulador + guía)
├── .gitignore                      ← exclusiones para Git
├── index.html                      ← aplicación
└── docs/
    ├── guia-ejercicios/
    │   ├── guia-ejercicios.tex     ← guía académica en LaTeX
    │   ├── Makefile                ← compila solo la guía
    │   ├── bibliografia.bib        ← referencias BibTeX (opcional)
    │   └── README.md               ← instrucciones de compilación
    └── capturas/
        └── .gitkeep                ← placeholder de capturas
```

### Archivos principales

| Archivo | Descripción |
|---------|-------------|
| `index.html` | aplicación con layout de 3 columnas. |
| `docs/guia-ejercicios/guia-ejercicios.tex` | Guía de ejercicios académica (portada, marco teórico, 6 bloques de ejercicios, apéndices, bibliografía). |
| `Makefile` | Compila el PDF de la guía y sirve el simulador localmente. |
| `LICENSE` | Texto legal completo de la GNU GPL v3. |

---

## 4. Controles

### Ratón / trackpad (versión escritorio y universal)

| Acción | Resultado |
|--------|-----------|
| Mover sliders | Ajustar parámetros físicos en tiempo real |
| Clic en **Pausar** | Detener / reanudar la simulación |
| Clic en **Reiniciar** | Volver el objeto al ángulo inicial y borrar la estela |
| Clic en **Modo TV** | Ocultar paneles y mostrar solo la simulación |
| Clic en **Pantalla completa** | Activar modo inmersivo |

### Teclado (versión universal)

| Tecla | Acción |
|-------|--------|
| `Espacio` | Pausar / reanudar |
| `R` | Reiniciar simulación |
| `F` | Activar / desactivar modo TV |
| `F11` | Pantalla completa |
| `↑` / `↓` | Aumentar / disminuir velocidad angular (ω) |
| `←` / `→` | Aumentar / disminuir longitud de la cuerda (r) |

### Touch (versión móvil)

| Gesto | Resultado |
|-------|-----------|
| Deslizar slider | Ajustar parámetro |
| Tocar pestaña | Cambiar entre Simulación / Controles / Resultados |
| Tocar botón | Ejecutar acción (pausa, reinicio) |

### Parámetros ajustables

| Parámetro | Rango | Unidad | Símbolo |
|-----------|-------|--------|---------|
| Longitud de la cuerda | 0.5 – 3.0 | metros | `r` |
| Velocidad angular | 0.5 – 10.0 | rad/s | `ω` |
| Masa del objeto | 0.1 – 10.0 | kilogramos | `m` |
| Velocidad de simulación | 0.1 – 3.0 | factor | — |

---

## 5. Arquitectura del código

Cada archivo HTML es autocontenido y se divide en secciones numeradas y comentadas:

| Sección | Contenido |
|---------|-----------|
| 1. HTML | Estructura semántica (controles, canvas, panel de resultados). |
| 2. CSS | Estilos, variables CSS, responsive, modo TV. |
| 3. Estado global | Variables de animación (`angle`, `paused`, `trail`). |
| 4. Controles | Referencias a sliders y botones, listeners de eventos. |
| 5. Cálculos físicos | Función `updateValues()` con todas las fórmulas. |
| 6. Renderizado | Función `drawArrow()` para los vectores. |
| 7. Bucle principal | `animate()` con `requestAnimationFrame`, integración temporal. |
| 8. Interacción | Listeners de teclado, touch y pantalla completa. |
| 9. Arranque | `resize`, primer frame, actualización inicial de valores. |

### Flujo de la animación

1. Se calcula `dt` (delta de tiempo) desde el frame anterior.
2. Se actualiza el ángulo: `angle += ω · dt · speed`.
3. Se calcula la posición del objeto: `x = cx + r·scale·cos(angle)`, `y = cy + r·scale·sin(angle)`.
4. Se limpia el canvas y se dibujan en orden: grid, trayectoria, estela, cuerda, pivote, objeto, vectores.
5. Se llama a `requestAnimationFrame` para el siguiente frame.

---

## 6. Modelo físico

### Magnitudes cinemáticas

| Magnitud | Fórmula | Unidad |
|----------|---------|--------|
| Velocidad tangencial | `v = ω · r` | m/s |
| Aceleración centrípeta | `ac = ω² · r` | m/s² |
| Período | `T = 2π / ω` | s |
| Frecuencia | `f = 1 / T` | Hz |
| Frecuencia en RPM | `RPM = f · 60` | rpm |

### Magnitudes dinámicas

| Magnitud | Fórmula | Unidad |
|----------|---------|--------|
| Fuerza centrípeta | `Fc = m · ac = m · ω² · r` | N |
| Tensión de la cuerda | `T = Fc` (en MCU horizontal) | N |
| Energía cinética | `Ec = ½ · m · v²` | J |
| Momento angular | `L = m · v · r` | kg·m²/s |

### Escalado de vectores en pantalla

Para que los vectores sean visibles sin distorsionar la simulación, se aplican factores de escala independientes:

```javascript
const vScale = 14;    // píxeles por (m/s)
const fScale = 2;     // píxeles por Newton
const acScale = 3;    // píxeles por (m/s²)
```

### Suposiciones del modelo
- Movimiento circular uniforme (MCU) en un plano horizontal.
- Cuerda inextensible y de masa despreciable.
- Ausencia de gravedad (o gravedad compensada, como en una mesa sin fricción).
- Sin rozamiento ni resistencia del aire.
- El pivote es un punto fijo ideal.

---

## 7. Personalización

### Cambiar colores de los vectores

Busca en la función `animate()` las llamadas a `drawArrow()`:

```javascript
drawArrow(px, py, px + vx, py + vy, '#ff5252', 'v');     // velocidad
drawArrow(px, py, px + fcx, py + fcy, '#4caf50', 'Fc');  // fuerza
drawArrow(px, py, px + acx, py + acy, '#ffeb3b', 'ac');  // aceleración
```

Sustituye los códigos hexadecimales por los colores que prefieras.

### Añadir nuevas magnitudes

1. Calcula la magnitud en `updateValues()`:
   ```javascript
   const nuevaMagnitud = ...; // tu fórmula
   ```
2. Añade un elemento HTML en el panel de resultados:
   ```html
   <div class="result">
     <div class="label">Nombre de la magnitud</div>
     <div class="val" id="nuevaVal">0.00<span class="unit">unidad</span></div>
   </div>
   ```
3. Actualiza su contenido:
   ```javascript
   document.getElementById('nuevaVal').innerHTML = 
     nuevaMagnitud.toFixed(2) + '<span class="unit">unidad</span>';
   ```

### Modificar los rangos de los sliders

Cada slider tiene atributos `min`, `max` y `step`:

```html
<input type="range" id="omega" min="0.5" max="10" step="0.1" value="3">
```

Ajusta estos valores según el rango físico que quieras explorar. Recuerda actualizar también las validaciones en los atajos de teclado si usas la versión universal.

---

## 8. Documentación académica

El proyecto incluye una guía de ejercicios académica en LaTeX pensada para usar el simulador como laboratorio virtual en cursos de física de nivel medio superior o superior.

### Contenido de la guía

| Sección | Descripción |
|---------|-------------|
| Portada institucional | Con datos del autor, institución, asignatura y fecha. |
| Resumen y palabras clave | Resumen ejecutivo del material didáctico. |
| Presentación | Objetivos de aprendizaje y cómo usar la guía. |
| Marco teórico | Movimiento circular uniforme, aceleración centrípeta, fuerza centrípeta, energía cinética rotacional, momento angular. |
| Bloque 0 | Familiarización con el simulador y sus controles. |
| Bloque 1 | Tablas de magnitudes para distintos valores de `r`, `ω` y `m`. |
| Bloque 2 | Verificación de `v = ω·r` y `ac = ω²·r` mediante mediciones. |
| Bloque 3 | Relación entre Fc y ω: demostrar que Fc ∝ ω². |
| Bloque 4 | Energía cinética y momento angular: conservación. |
| Bloque 5 | Aplicaciones: curvas en vehículos, centrifugadoras, atracciones de feria. |
| Bloque 6 | Proyecto final: diseñar un experimento virtual y presentar conclusiones. |
| Apéndices | Constantes y fórmulas, datos de referencia para el docente, rúbrica de evaluación. |
| Bibliografía | Referencias (Resnick, Sears, Khan Academy, HyperPhysics). |

### Compilar la guía

#### Requisitos
- **TeX Live** (Linux/macOS) o **MiKTeX** (Windows), con los paquetes `babel-spanish`, `siunitx`, `tcolorbox`, `longtable`, `fancyhdr`, `hyperref`.
- **Overleaf** (alternativa sin instalación).

#### Compilación local
```bash
# Desde la raíz del proyecto
make guia

# O manualmente
cd docs/guia-ejercicios
pdflatex guia-ejercicios.tex
pdflatex guia-ejercicios.tex   # segunda pasada para referencias e índice
```

El PDF resultante queda en `docs/guia-ejercicios/guia-ejercicios.pdf`.

#### Compilación en Overleaf
1. Crea un proyecto vacío en [https://www.overleaf.com](https://www.overleaf.com).
2. Sube `docs/guia-ejercicios/guia-ejercicios.tex`.
3. Pulsa Recompile.

### Personalizar la guía

Busca el bloque "DATOS DEL AUTOR" al inicio de `guia-ejercicios.tex`:

```latex
\newcommand{\autor}{<<TU NOMBRE COMPLETO>>}
\newcommand{\institucion}{<<TU INSTITUCIÓN / UNIVERSIDAD>>}
\newcommand{\facultad}{<<FACULTAD / DEPARTAMENTO>>}
\newcommand{\asignatura}{<<ASIGNATURA / CURSO>>}
\newcommand{\profesor}{<<PROFESOR / TUTOR>>}
\newcommand{\correo}{<<tu.correo@institucion.edu>>}
\newcommand{\ciudad}{<<CIUDAD, PAÍS>>}
```

Sustituye cada `<<...>>` por tus datos.

---

## 9. Roadmap

- [x] Simulación básica de MCU con vectores de velocidad y fuerza.
- [x] Panel de resultados físicos en tiempo real.
- [x] Versión para escritorio (`simulador.html`).
- [x] Versión para smartphone (`simulador-mobile.html`).
- [x] Versión universal con modo TV y pantalla completa (`simulador-universal.html`).
- [x] Atajos de teclado y soporte HiDPI.
- [x] Guía de ejercicios académica en LaTeX.
- [ ] Movimiento circular no uniforme (con aceleración angular α).
- [ ] Vector de aceleración tangencial cuando ω varía.
- [ ] Modo "péndulo cónico" con gravedad y ángulo de la cuerda.
- [ ] Exportar datos a CSV para análisis externo.
- [ ] Gráficas en tiempo real de v(t), Fc(t), ac(t).
- [ ] Comparación entre MCU y MCUV lado a lado.
- [ ] Versión en inglés de la interfaz y de la guía.
- [ ] Persistencia del estado en `localStorage`.
- [ ] Migración opcional a WebGL para miles de partículas.

---

## 10. Limitaciones conocidas

- **Modelo idealizado**: no incluye rozamiento, gravedad ni deformación de la cuerda.
- **Integración explícita simple**: el ángulo se actualiza como `angle += ω·dt`, sin corrección de errores de acumulación a largo plazo (no crítico en MCU).
- **Vectores escalados artificialmente**: los factores de escala son fijos para garantizar visibilidad; no representan magnitudes a escala real entre sí.
- **Canvas 2D**: adecuado para un solo objeto; no optimizado para sistemas de muchas partículas.
- **Sin persistencia**: el estado de los controles no se guarda entre sesiones (puede añadirse con `localStorage`).

---

## 11. Contribuir

Este proyecto es software libre bajo GPL v3 y todas las contribuciones son bienvenidas.

1. Haz fork del repositorio.
2. Crea una rama: `git checkout -b feature/nueva-funcionalidad`.
3. Haz commit: `git commit -m "feat: descripción del cambio"`.
4. Haz push: `git push origin feature/nueva-funcionalidad`.
5. Abre un pull request.

### Buenas prácticas

- Mantén el estilo del código (comentarios numerados por sección).
- Si añades una nueva magnitud física, documenta su fórmula en la sección 6.
- Si modificas el motor, actualiza esta documentación (`README.md`).
- Si modificas la guía, recompila el PDF antes de hacer commit.
- Prueba los tres archivos HTML antes de hacer commit.
- Al ser GPL v3, tus contribuciones se integrarán bajo la misma licencia.

### Ideas especialmente buscadas

- Implementación de movimiento circular no uniforme.
- Modo péndulo cónico con análisis de fuerzas en 3D.
- Gráficas en tiempo real con Chart.js o similar.
- Traducción de la interfaz y la guía al inglés, francés o portugués.
- Versión para realidad aumentada (WebXR).

---

## 12. Referencias

1. **Resnick, Halliday & Krane** — *Física*, vol. 1, cap. 6: Movimiento circular.
2. **Sears, Zemansky & Young** — *Universidad con Física Moderna*, unidades de dinámica circular.
3. **Khan Academy** — *Intro to motion in circles*: [https://www.khanacademy.org/science/physics/centripetal-forces-and-gravitation](https://www.khanacademy.org/science/physics/centripetal-forces-and-gravitation)
4. **PhET Interactive Simulations** — *Ladybug Revolution, Motion in 2D*: [https://phet.colorado.edu](https://phet.colorado.edu)
5. **HyperPhysics** — *Circular Motion*: [http://hyperphysics.phy-astr.gsu.edu/hbase/circmot.html](http://hyperphysics.phy-astr.gsu.edu/hbase/circmot.html)
6. **MDN Web Docs** — *Canvas API*: [https://developer.mozilla.org/docs/Web/API/Canvas_API](https://developer.mozilla.org/docs/Web/API/Canvas_API)

---

## 13. Autor

**MTI. Juan Carlos Santiago Sánchez**

- GitHub: [@jcteacher-lab](https://github.com/jcteacher-lab)
- Correo: juancarlos.santiago.cb161@dgeti.sems.gob.mx

---

## 14. Licencia

**Simulador de Movimiento Circular**

Copyright (C) 2026

Este programa es software libre: puedes redistribuirlo y/o modificarlo bajo los términos de la GNU General Public License tal como la publica la Free Software Foundation, ya sea la versión 3 de la Licencia, o (a tu elección) cualquier versión posterior.

Este programa se distribuye con la esperanza de que sea útil, pero **SIN NINGUNA GARANTÍA**; ni siquiera la garantía implícita de COMERCIABILIDAD o IDONEIDAD PARA UN PROPÓSITO PARTICULAR. Consulta la GNU General Public License para más detalles.

Deberías haber recibido una copia de la GNU General Public License junto con este programa. Si no es así, consulta [https://www.gnu.org/licenses/](https://www.gnu.org/licenses/).

### Resumen de la licencia

|  |  |
|--|--|
| Licencia | GNU General Public License v3.0 |
| SPDX | GPL-3.0-or-later |
| Copyright | (C) 2026 |
| Texto legal completo | [LICENSE](./LICENSE) · [gnu.org/licenses/gpl-3.0](https://www.gnu.org/licenses/gpl-3.0.txt) |

> **Importante**: para que el proyecto esté correctamente licenciado bajo GPL v3, además de este `README.md` debes incluir en la raíz del repositorio un archivo llamado `LICENSE` (sin extensión) con el texto legal completo. Puedes obtenerlo con:
> ```bash
> curl -o LICENSE https://www.gnu.org/licenses/gpl-3.0.txt
> ```

---

## 15. Agradecimientos

Inspirado en los simuladores educativos de PhET Interactive Simulations (Universidad de Colorado) y en la larga tradición de recursos abiertos para la enseñanza de la física. Construido con la idea de que cualquier docente o estudiante pueda extenderlo, modificarlo y adaptarlo a sus necesidades sin depender de software propietario.

---

## 16. Proyectos relacionados

- [**Simulador del Sistema Solar**](https://jcteacher-lab.github.io/sistemasolar/) — Simulador interactivo del Sistema Solar con órbitas keplerianas reales (elementos J2000), panel de datos físicos y guía de ejercicios en LaTeX.
- [**Simulador de Tiro Parabólico**](https://jcteacher-lab.github.io/tiroparabolico) — Simulador educativo de movimiento de proyectiles con Canvas 2D.
- [**Analizador de parábolas**](https://github.com/jcteacher-lab/analizadordeparabolas) — Herramienta didáctica para explorar la parábola: cambia a, h y k con deslizadores y observa cómo se traslada el vértice.
- [**Graficador dinámico de parábolas**](https://github.com/jcteacher-lab/Graficador_dinamico_parabolas) — Simulador educativo que construye la gráfica y la ecuación de una parábola a partir de sus elementos geométricos: Vértice, Foco y Directriz.

---

> *"La física no es solo fórmulas: es ver el mundo moverse y entender por qué."*

Hecho con ❤️ y con libertad — GPL v3 garantiza que seguirá siendo libre.
