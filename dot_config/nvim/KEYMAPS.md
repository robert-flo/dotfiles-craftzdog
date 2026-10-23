# ⌨️ Guía Completa de Atajos de Teclado (Craftzdog Neovim)

> **Nota sobre la tecla Leader**: En esta configuración, `<Leader>` es la barra espaciadora (`Space`).  
> No hay menú emergente visual (sin `which-key`); los comandos se ejecutan presionando la secuencia directamente.

---

## ⚡ 1. LO MÁS BÁSICO (Día a Día)

Los atajos imprescindibles que utilizarás el 90% del tiempo:

| Atajo | Acción | Descripción |
| :--- | :--- | :--- |
| **`;f`** | **Buscar archivos** | Abre el buscador difuso de archivos (`Snacks Picker`) |
| **`;r`** | **Buscar texto (Live Grep)** | Busca cualquier texto en todo el proyecto |
| **`sf`** | **Explorador de archivos** | Abre el explorador flotante interactivo (`Oil.nvim`) |
| **`\\`** | **Buffers abiertos** | Muestra la lista de archivos/pestañas abiertas |
| **`;;`** | **Reanudar búsqueda** | Vuelve a abrir el último menú de búsqueda cerrado |
| **`;g`** | **Lazygit** | Abre la interfaz completa de Git |
| **`<Space>f`** | **Formatear código** | Formatea el archivo actual con `conform` (Prettier, Oxlint, etc.) |
| **`ss`** | **Dividir ventana horizontal** | Divide la pantalla arriba / abajo |
| **`sv`** | **Dividir ventana vertical** | Divide la pantalla izquierda / derecha |
| **`sh` / `sj` / `sk` / `sl`** | **Moverse entre ventanas** | Salta a la ventana Izquierda / Abajo / Arriba / Derecha |
| **`te`** | **Nueva pestaña** | Abre una pestaña limpia (`:tabedit`) |
| **`<Tab>` / `<S-Tab>`** | **Navegar pestañas** | Salta a la pestaña siguiente o anterior |

---

## 🛠️ 2. DETALLADOS POR TIPO DE TAREA

### 📝 Edición y Manejo de Registros (Portapapeles Limpio)
Craftzdog previene que borrar texto contamine lo que acabas de copiar:

| Atajo | Modo | Acción |
| :--- | :---: | :--- |
| **`x`** | Normal | Borra un carácter sin guardarlo en el portapapeles (`"_x`) |
| **`dw`** | Normal | Borra la palabra hacia atrás sin guardarla en el portapapeles |
| **`<Ctrl> + a`** | Normal | Seleccionar todo el contenido del archivo |
| **`+` / `-`** | Normal | Incrementar / decrementar el número bajo el cursor |
| **`<Space>p` / `<Space>P`** | Normal / Visual | Pega lo último copiado con *yank* (registro `0`), ignorando lo borrado |
| **`<Space>c` / `<Space>C`** | Normal / Visual | Cambiar texto sin ensuciar registros de portapapeles |
| **`<Space>d` / `<Space>D`** | Normal / Visual | Borrar texto sin ensuciar registros de portapapeles |
| **`<Space>o` / `<Space>O`** | Normal | Inserta una línea vacía abajo/arriba sin continuar comentarios |
| **`<Space>yf`** | Normal | Copia al portapapeles la ruta relativa del archivo y la línea |
| **`<Space>yp`** | Normal | Copia al portapapeles la ruta absoluta del archivo y la línea |
| **`<Space>cc`** | Visual | Copia la selección con formato de bloque de código Markdown |
| **`<Space>j`** | Normal | Abre el `package.json` del proyecto en una ventana flotante |

---

### 🧠 Navegación de Código, LSP y Diagnósticos

| Atajo | Modo | Acción |
| :--- | :---: | :--- |
| **`gd`** | Normal | **Ir a la definición** del símbolo (abre picker de Snacks) |
| **`gD`** | Normal | Ir a la declaración |
| **`gy`** | Normal | Ir a la definición de tipo (*Type Definition*) |
| **`gr`** | Normal | Listar todas las referencias donde se usa el símbolo |
| **`gI`** | Normal | Ir a la implementación / definición de origen (*Source Definition*) |
| **`K`** | Normal | Ver documentación emergente (*Hover*) |
| **`gK`** | Normal | Ayuda de firma de la función (*Signature Help*) |
| **`<Ctrl> + k`** | Insertar | Ver ayuda de firma mientras escribes argumentos |
| **`<Ctrl> + j`** | Normal | Saltar al siguiente error o aviso de diagnóstico |
| **`<Space>ca`** | Normal / Visual | **Acciones de código** (*Code Actions* / Quick Fixes) |
| **`<Space>cr`** | Normal | **Renombrar símbolo** en todo el proyecto (*Rename*) |
| **`<Space>cR`** | Normal | Renombrar archivo actual y actualizar imports |
| **`<Space>cl`** | Normal | Ver información de servidores LSP activos |
| **`;e`** | Normal | Ver lista de diagnósticos y errores del proyecto |
| **`;c`** | Normal | Ver árbol de llamadas entrantes (*Incoming calls*) |
| **`]]` / `[[`** | Normal | Saltar a la siguiente / anterior referencia del símbolo actual |

---

### 🌿 Git y Control de Cambios

| Atajo | Modo | Acción |
| :--- | :---: | :--- |
| **`;g`** | Normal | **Abrir Lazygit** |
| **`;h`** | Normal | Ver lista interactiva de cambios pendientes (*Git Hunks*) |
| **`<Space>gb`** | Normal | Ver *Git blame* de la línea actual |
| **`<Space>gB`** | Normal | Ver *Git blame* de todo el archivo |
| **`<Space>go`** | Normal | Abrir el archivo en el commit histórico del blame |
| **`<Space>gs`** | Normal | Alternar Stage/Unstage de todo el buffer |
| **`<Space>gh`** | Normal | Alternar Stage/Unstage del bloque (*hunk*) actual |
| **`<Space>gd`** | Normal | Alternar vista superpuesta de diferencias (`MiniDiff`) |
| **`<Space>dv`** | Normal | Abrir comparador interactivo de código (`CodeDiff`) |
| **`<Space>dh`** | Normal | Historial de git del archivo actual |
| **`<Space>dH`** | Normal | Historial de git de todo el repositorio |
| **`]c` / `[c`** | Normal | Saltar al cambio git siguiente / anterior en el archivo |

---

### 📂 Navegación en el Explorador de Archivos (`Oil.nvim` con `sf`)
Al presionar **`sf`** se abre un buffer editable que representa tu sistema de archivos:

| Tecla | Acción |
| :---: | :--- |
| **`Enter`** | Abrir archivo o entrar a carpeta |
| **`h`** | Subir un nivel de directorio (directorio padre) |
| **`q`** | Cerrar el explorador |
| **`:w`** | Guarda cambios: ¡puedes renombrar o borrar archivos editando texto normal y guardando! |

---

### 🤖 GitHub Copilot y Autocompletado

| Atajo | Modo | Acción |
| :--- | :---: | :--- |
| **`<Enter>` o `<Ctrl> + y`** | Insertar | Aceptar sugerencia del menú de completado (`blink.cmp`) |
| **`<Ctrl> + l`** | Insertar | Aceptar sugerencia gris de Copilot |
| **`<Alt> + l`** | Insertar | Aceptar solo la siguiente palabra sugerida por Copilot |
| **`<Alt> + Shift + l`** | Insertar | Aceptar la línea completa sugerida por Copilot |
| **`<Alt> + ]` / `<Alt> + [`** | Insertar | Siguiente / anterior sugerencia alternativa de Copilot |
| **`<Ctrl> + ]`** | Insertar | Descartar sugerencia actual de Copilot |

---

### 🪟 Gestión de Ventanas y Buffers

| Atajo | Modo | Acción |
| :--- | :---: | :--- |
| **`ss`** | Normal | Dividir ventana en horizontal |
| **`sv`** | Normal | Dividir ventana en vertical |
| **`sh` / `sj` / `sk` / `sl`** | Normal | Mover foco de ventana (Izquierda / Abajo / Arriba / Derecha) |
| **`te`** | Normal | Abrir nueva pestaña |
| **`<Tab>` / `<S-Tab>`** | Normal | Cambiar entre pestañas |
| **`\\`** | Normal | Listar y cambiar entre buffers abiertos |
| **`<Space>bd`** | Normal | Cerrar buffers ocultos en segundo plano |
