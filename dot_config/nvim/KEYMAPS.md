# ⌨️ Guía de Atajos de Teclado (Craftzdog Neovim)

> ⚠️ **IMPORTANTE**:  
> - Los atajos marcados con **`[CON <space>]`** requieren pulsar primero la barra espaciadora y luego la tecla (ejemplo: `<space>` seguido de `f`).
> - Los atajos marcados con **`[SIN <space>]`** se pulsan **DIRECTAMENTE**. Por ejemplo, **`;r` es solo la tecla `;` seguida de la tecla `r`** (NUNCA pulses `<space>` antes de `;r`).

---

## ⚡ 1. LO MÁS BÁSICO (Día a Día)

| ¿Lleva `<space>`? | Combinación exacta | Qué hace |
| :---: | :--- | :--- |
| ❌ **NO** | **`;f`** *(tecla `;` y luego `f`)* | **Buscar archivos** en el proyecto (`Snacks Picker`) |
| ❌ **NO** | **`;r`** *(tecla `;` y luego `r`)* | **Buscar texto (Live Grep)** en todo el proyecto |
| ❌ **NO** | **`sf`** *(tecla `s` y luego `f`)* | **Explorador de archivos** flotante interactivo (`Oil`) |
| ❌ **NO** | **`\\`** *(dos barras invertidas)* | **Listar buffers/archivos abiertos** |
| ❌ **NO** | **`;;`** *(dos puntos y coma)* | **Reanudar** la última búsqueda que cerraste |
| ❌ **NO** | **`;g`** *(tecla `;` y luego `g`)* | **Abrir Lazygit** |
| ✅ **SÍ** | **`<space> + f`** | **Formatear código** con Prettier / Oxlint / Stylua |
| ❌ **NO** | **`ss`** *(dos veces la tecla `s`)* | **Dividir ventana en horizontal** (arriba / abajo) |
| ❌ **NO** | **`sv`** *(tecla `s` y luego `v`)* | **Dividir ventana en vertical** (izquierda / derecha) |
| ❌ **NO** | **`sh`** / **`sj`** / **`sk`** / **`sl`** | **Moverse de ventana** (Izquierda / Abajo / Arriba / Derecha) |
| ❌ **NO** | **`te`** *(tecla `t` y luego `e`)* | **Nueva pestaña** limpia (`:tabedit`) |
| ❌ **NO** | **`<Tab>`** / **`<Shift> + <Tab>`** | Cambiar a pestaña **siguiente** / **anterior** |

---

## 🛠️ 2. DETALLADOS POR TIPO DE TAREA

---

### 📝 Edición y Manejo del Portapapeles (Yank / Pegar / Borrar)

| ¿Lleva `<space>`? | Combinación exacta | Modo | Qué hace |
| :---: | :--- | :---: | :--- |
| ✅ **SÍ** | **`<space> + p`** | Normal / Visual | **Pegar lo último copiado**: usa el registro `0`, ignorando lo que hayas borrado con `d` o `x` |
| ✅ **SÍ** | **`<space> + P`** | Normal | Pegar antes del cursor desde el registro `0` |
| ✅ **SÍ** | **`<space> + c`** | Normal / Visual | Cambiar texto **sin** sobreescribir el portapapeles |
| ✅ **SÍ** | **`<space> + C`** | Normal / Visual | Cambiar hasta el fin de línea sin sobreescribir portapapeles |
| ✅ **SÍ** | **`<space> + d`** | Normal / Visual | Borrar texto **sin** sobreescribir el portapapeles |
| ✅ **SÍ** | **`<space> + D`** | Normal / Visual | Borrar hasta el fin de línea sin sobreescribir portapapeles |
| ✅ **SÍ** | **`<space> + o`** | Normal | Insertar línea abajo limpia (sin autocompletar comentarios `//` o `#`) |
| ✅ **SÍ** | **`<space> + O`** | Normal | Insertar línea arriba limpia (sin autocompletar comentarios) |
| ✅ **SÍ** | **`<space> + yf`** | Normal | Copiar al portapapeles la ruta relativa del archivo y línea (ej. `src/index.ts:42`) |
| ✅ **SÍ** | **`<space> + yp`** | Normal | Copiar al portapapeles la ruta absoluta del archivo y línea |
| ✅ **SÍ** | **`<space> + cc`** | Visual | Copiar selección formateada como bloque de código Markdown (\`\`\`lenguaje) |
| ✅ **SÍ** | **`<space> + j`** | Normal | Abrir el archivo `package.json` en una ventana flotante |
| ❌ **NO** | **`x`** | Normal | Borrar un solo carácter sin ensuciar portapapeles |
| ❌ **NO** | **`dw`** | Normal | Borrar palabra hacia atrás sin ensuciar portapapeles |
| ❌ **NO** | **`<Ctrl> + a`** | Normal | Seleccionar todo el archivo |
| ❌ **NO** | **`+`** / **`-`** | Normal | Incrementar / decrementar el número bajo el cursor |

---

### 🧠 Intellisense, LSP y Diagnósticos

| ¿Lleva `<space>`? | Combinación exacta | Modo | Qué hace |
| :---: | :--- | :---: | :--- |
| ✅ **SÍ** | **`<space> + ca`** | Normal / Visual | **Acciones de código** (*Code Actions* / Quick Fixes) |
| ✅ **SÍ** | **`<space> + cr`** | Normal | **Renombrar símbolo** en todo el proyecto (*LSP Rename*) |
| ✅ **SÍ** | **`<space> + cR`** | Normal | Renombrar archivo físico y actualizar imports automáticamente |
| ✅ **SÍ** | **`<space> + cc`** | Normal / Visual | Ejecutar CodeLens bajo el cursor |
| ✅ **SÍ** | **`<space> + cC`** | Normal | Refrescar CodeLens en el buffer |
| ✅ **SÍ** | **`<space> + cl`** | Normal | Ver información de los servidores LSP activos |
| ❌ **NO** | **`gd`** | Normal | **Ir a definición** del símbolo bajo el cursor |
| ❌ **NO** | **`gD`** | Normal | Ir a declaración del símbolo |
| ❌ **NO** | **`gy`** | Normal | Ir a definición de tipo (*Type Definition*) |
| ❌ **NO** | **`gr`** | Normal | Listar todas las referencias donde se usa el símbolo |
| ❌ **NO** | **`gI`** | Normal | Ir al código fuente original (*Source Definition*) |
| ❌ **NO** | **`K`** | Normal | Ver documentación emergente (*Hover*) |
| ❌ **NO** | **`gK`** | Normal | Ver ayuda de firma (*Signature Help*) |
| ❌ **NO** | **`<Ctrl> + k`** | Insertar | Ver argumentos de la función mientras escribes |
| ❌ **NO** | **`<Ctrl> + j`** | Normal | Saltar al siguiente error/advertencia en el archivo |
| ❌ **NO** | **`;e`** | Normal | Listar todos los diagnósticos y errores del proyecto |
| ❌ **NO** | **`;c`** | Normal | Listar llamadas entrantes a esta función (*Incoming calls*) |
| ❌ **NO** | **`]]`** / **`[[`** | Normal | Saltar a la siguiente / anterior referencia del símbolo |

---

### 🌿 Git y Control de Versiones

| ¿Lleva `<space>`? | Combinación exacta | Modo | Qué hace |
| :---: | :--- | :---: | :--- |
| ❌ **NO** | **`;g`** | Normal | **Abrir Lazygit** |
| ❌ **NO** | **`;h`** | Normal | Ver lista interactiva de cambios pendientes (*Git Hunks*) |
| ✅ **SÍ** | **`<space> + gb`** | Normal | Ver *Git blame* de la línea actual |
| ✅ **SÍ** | **`<space> + gB`** | Normal | Ver *Git blame* de todo el archivo |
| ✅ **SÍ** | **`<space> + go`** | Normal | Abrir el archivo en una nueva pestaña en el commit del blame |
| ✅ **SÍ** | **`<space> + gs`** | Normal | Alternar Stage/Unstage de todo el archivo |
| ✅ **SÍ** | **`<space> + gh`** | Normal | Alternar Stage/Unstage del bloque (*hunk*) actual |
| ✅ **SÍ** | **`<space> + gd`** | Normal | Alternar vista superpuesta de diferencias (`MiniDiff`) |
| ✅ **SÍ** | **`<space> + dv`** | Normal | Abrir comparador interactivo de código (`CodeDiff`) |
| ✅ **SÍ** | **`<space> + dh`** | Normal | Historial de commits del archivo actual |
| ✅ **SÍ** | **`<space> + dH`** | Normal | Historial de commits de todo el repositorio |
| ❌ **NO** | **`]c`** / **`[c`** | Normal | Saltar al cambio git siguiente / anterior |

---

### 📂 Explorador de Archivos (`Oil.nvim` con `sf`)
*Pulsa `sf` (sin `<space>`) para abrirlo. Una vez dentro de la ventana de Oil:*

| ¿Lleva `<space>`? | Tecla | Qué hace |
| :---: | :---: | :--- |
| ❌ **NO** | **`<Enter>`** | Abrir archivo seleccionado o entrar a la carpeta |
| ❌ **NO** | **`h`** | Subir al directorio padre |
| ❌ **NO** | **`q`** | Cerrar el explorador |
| ❌ **NO** | **`:w`** | Guardar cambios: ¡puedes renombrar, mover o borrar archivos simplemente editando el texto del buffer y guardando con `:w`! |

---

### 🤖 GitHub Copilot y Autocompletado (`blink.cmp`)

| ¿Lleva `<space>`? | Combinación exacta | Modo | Qué hace |
| :---: | :--- | :---: | :--- |
| ❌ **NO** | **`<Enter>`** o **`<Ctrl> + y`** | Insertar | Aceptar la sugerencia del menú de completado (`blink.cmp`) |
| ❌ **NO** | **`<Ctrl> + l`** | Insertar | Aceptar toda la sugerencia gris de Copilot |
| ❌ **NO** | **`<Alt> + l`** | Insertar | Aceptar solo la siguiente palabra de Copilot |
| ❌ **NO** | **`<Alt> + Shift + l`** | Insertar | Aceptar la línea completa sugerida por Copilot |
| ❌ **NO** | **`<Alt> + ]`** / **`<Alt> + [`** | Insertar | Siguiente / anterior alternativa de Copilot |
| ❌ **NO** | **`<Ctrl> + ]`** | Insertar | Descartar la sugerencia de Copilot |

---

### 🪟 Ventanas, Pestañas y Buffers

| ¿Lleva `<space>`? | Combinación exacta | Modo | Qué hace |
| :---: | :--- | :---: | :--- |
| ❌ **NO** | **`ss`** | Normal | Dividir ventana en horizontal (arriba / abajo) |
| ❌ **NO** | **`sv`** | Normal | Dividir ventana en vertical (izquierda / derecha) |
| ❌ **NO** | **`sh`** / **`sj`** / **`sk`** / **`sl`** | Normal | Mover foco de ventana (Izquierda / Abajo / Arriba / Derecha) |
| ❌ **NO** | **`te`** | Normal | Abrir nueva pestaña |
| ❌ **NO** | **`<Tab>`** / **`<Shift> + <Tab>`** | Normal | Cambiar entre pestañas abierta |
| ❌ **NO** | **`\\`** | Normal | Listar y cambiar entre buffers abiertos |
| ✅ **SÍ** | **`<space> + bd`** | Normal | Cerrar todos los buffers en segundo plano que no estén en pantalla |
