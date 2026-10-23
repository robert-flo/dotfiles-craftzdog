# 🗺️ Mapa de Arquitectura y Guía de Réplica: De Cero a Craftzdog Neovim

Esta guía desglosa paso a paso cómo está construida la configuración de Craftzdog Neovim (versión 0.12+ con `vim.pack`) y la ruta exacta para construir tu propia configuración (`rvim`) archivo por archivo, entendiendo el porqué de cada pieza.

---

## 🏛️ Mapa Completo de la Arquitectura

```
dot_config/nvim/
├── init.lua                          # 🚪 Entrada principal (carga ordenadamente los módulos)
├── KEYMAPS.md                        # ⌨️ Chuleta completa de atajos de teclado
├── ARCHITECTURE_ROADMAP.md           # 🗺️ Este mapa arquitectónico
├── after/lsp/                        # 🔌 Configuraciones especializadas por servidor LSP
│   ├── cssls.lua                     # CSS / Tailwind
│   ├── lua_ls.lua                    # Lua para Neovim
│   ├── oxlint.lua                    # Linter ultra rápido en Rust (Oxlint)
│   └── vtsls.lua                     # TypeScript Language Server de alto rendimiento
└── lua/craftzdog/
    ├── config/                       # ⚙️ 1. NÚCLEO NATIVO (Sin plugins, Neovim puro)
    │   ├── options.lua               # Opciones globales (tabs, números de línea, etc.)
    │   ├── keymaps.lua               # Atajos nativos (splits, tabs, moverse de ventana)
    │   ├── autocmds.lua              # Eventos automáticos (resaltado al copiar, cursorline)
    │   ├── commands.lua              # Comandos personalizados en consola (:ToggleFormatter)
    │   └── workarounds.lua           # Ajustes finos de compatibilidad
    ├── utils/                        # 🧰 2. CAJA DE HERRAMIENTAS Y HELPERS
    │   ├── init.lua                  # Expone los utilitarios en la variable global _G.Craftzdog
    │   ├── icons.lua                 # Diccionario centralizado de iconos Nerd Font
    │   ├── editor.lua                # Funciones para copiar rutas, abrir package.json, buffers
    │   ├── lazygit.lua               # Wrapper para abrir Lazygit en ventana flotante
    │   ├── lualine.lua               # Componentes dinámicos de la barra de estado
    │   └── tabline.lua               # Renderizado visual de pestañas superiores
    └── plugins/                      # 📦 3. GESTIÓN Y CONFIGURACIÓN DE PLUGINS
        ├── init.lua                  # Lista declarativa de plugins vía `vim.pack.add`
        ├── ui.lua                    # Tema Solarized Osaka, lualine, incline, trouble, codediff
        ├── treesitter.lua            # Resaltado sintáctico AST y navegación por nodos
        ├── editor.lua                # Autocompletado (blink.cmp), formato (conform), mini.pairs
        ├── lsp.lua                   # mason, mason-tool-installer, nvim-lspconfig
        ├── util.lua                  # Explorador editable (oil.nvim) y Copilot
        └── keymaps.lua               # Atajos de teclado que dependen de plugins (Snacks, LSP)
```

---

## 🧭 Plan de Replicación Paso a Paso (Para `rvim`)

Para construir tu configuración `rvim` sin que se rompa nada en el camino, sigue este orden secuencial:

```
[Fase 1: El Núcleo] ➡️ [Fase 2: Utilitarios] ➡️ [Fase 3: Gestor y Tema] ➡️ [Fase 4: Navegación] ➡️ [Fase 5: Motor de Edición] ➡️ [Fase 6: LSP]
```

---

### 🟢 FASE 1: El Núcleo Nativo (Vanilla Neovim)
*Objetivo: Tener un editor cómodo, rápido y bien configurado antes de instalar un solo plugin.*

1. **`init.lua`**:
   - Activa el cargador rápido nativo:
     ```lua
     if vim.loader then vim.loader.enable() end
     ```
   - Llama en orden a los módulos de configuración:
     ```lua
     require("rvim.config.options")
     require("rvim.config.keymaps")
     require("rvim.config.autocmds")
     require("rvim.config.commands")
     ```
2. **`lua/rvim/config/options.lua`**:
   - Define variables como `vim.g.mapleader = " "`.
   - Configura identación a 2 espacios (`tabstop`, `shiftwidth`, `expandtab`).
   - Habilita `termguicolors`, `number`, `relativenumber`, `signcolumn = "yes"`.
   - Configura el portapapeles compartido: `vim.opt.clipboard = "unnamedplus"`.
3. **`lua/rvim/config/keymaps.lua`**:
   - Atajos nativos de ventanas: `ss` (split horizontal), `sv` (split vertical).
   - Movimiento entre ventanas: `sh`, `sj`, `sk`, `sl`.
   - Pestañas: `te` (`:tabedit<CR>`), `<Tab>` y `<S-Tab>`.
   - Protección de portapapeles: `x -> "_x`, `<Leader>p -> "0p`.
4. **`lua/rvim/config/autocmds.lua`**:
   - Resaltado temporal al copiar texto (`TextYankPost`).
   - Activar `cursorline` solo en la ventana activa (`WinEnter` / `WinLeave`).
5. **`lua/rvim/config/commands.lua`**:
   - Comandos de usuario con `vim.api.nvim_create_user_command`.

---

### 🟡 FASE 2: La Caja de Herramientas (`utils/`)
*Objetivo: Centralizar funciones auxiliares e iconos para no repetir código en los plugins.*

1. **`lua/rvim/utils/icons.lua`**:
   - Tabla con glifos Nerd Font para diagnósticos (`Error`, `Warn`, `Info`), Git (`added`, `modified`, `removed`), tipos de LSP (`Function`, `Variable`, etc.).
2. **`lua/rvim/utils/editor.lua`**:
   - Funciones prácticas en Lua puro:
     - `yank_relative_path_with_line()`: Copia `src/app.ts:25`.
     - `delete_hidden_buffers()`: Cierra buffers que no están en ninguna ventana activa.
     - `open_package_json()`: Abre un buffer flotante rápido.
3. **`lua/rvim/utils/init.lua`**:
   - Importa y expone todo como módulo global para fácil acceso:
     ```lua
     _G.Rvim = require("rvim.utils")
     ```

---

### 🟠 FASE 3: El Gestor de Plugins y la Interfaz Visual
*Objetivo: Establecer `vim.pack` e instalar la estética visual característica.*

1. **`lua/rvim/plugins/init.lua`**:
   - Declarar función auxiliar:
     ```lua
     local gh = function(repo) return "https://github.com/" .. repo end
     ```
   - Registrar los plugins con el gestor nativo de Neovim 0.12:
     ```lua
     vim.pack.add({
       { src = gh("craftzdog/solarized-osaka.nvim") },
       { src = gh("nvim-mini/mini.icons") },
       { src = gh("nvim-lualine/lualine.nvim") },
       { src = gh("b0o/incline.nvim") },
     })
     ```
2. **`lua/rvim/plugins/ui.lua`**:
   - Configuración de colores:
     ```lua
     require("solarized-osaka").setup({ transparent = true })
     vim.cmd.colorscheme("solarized-osaka")
     ```
   - Configuración de `lualine`: barra inferior limpia con información de git, diagnósticos y modo actual.
   - Configuración de `incline.nvim`: pequeña etiqueta flotante en la esquina superior derecha que muestra el nombre del archivo activo.

---

### 🔵 FASE 4: Árbol Sintáctico, Búsqueda y Navegación
*Objetivo: Proporcionar resaltado de código de última generación y exploración de archivos.*

1. **Añadir a `plugins/init.lua`**:
   ```lua
   { src = gh("nvim-treesitter/nvim-treesitter") },
   { src = gh("stevearc/oil.nvim") },
   { src = gh("folke/snacks.nvim") },
   ```
2. **`lua/rvim/plugins/treesitter.lua`**:
   - Configurar `nvim-treesitter` con lista de parsers esenciales (`lua`, `typescript`, `tsx`, `javascript`, `html`, `css`, `json`, `markdown`, `bash`, `python`).
   - Activar `highlight = { enable = true }` e `indent = { enable = true }`.
3. **`lua/rvim/plugins/util.lua`**:
   - Configurar `oil.nvim`: explorador de archivos donde las carpetas son texto editable (atajo `sf`).
   - Configuración de `copilot.lua` (si se utiliza IA asistida).
4. **Vincular atajos en `lua/rvim/plugins/keymaps.lua`**:
   - `;f` -> `Snacks.picker.files` (Buscador de archivos difuso).
   - `;r` -> `Snacks.picker.grep` (Live Grep / búsqueda de texto).
   - `\\` -> `Snacks.picker.buffers` (Lista de buffers abiertos).

---

### 🟣 FASE 5: Motor de Edición y Control de Versiones
*Objetivo: Formateo automático, autocompletado y Git integrado.*

1. **Añadir a `plugins/init.lua`**:
   ```lua
   { src = gh("saghen/blink.cmp"), version = vim.version.range("^1") },
   { src = gh("stevearc/conform.nvim") },
   { src = gh("nvim-mini/mini.pairs") },
   { src = gh("lewis6991/gitsigns.nvim") },
   { src = gh("craftzdog/mini.diff") },
   { src = gh("folke/todo-comments.nvim") },
   ```
2. **`lua/rvim/plugins/editor.lua`**:
   - **`blink.cmp`**: Configurar el motor de autocompletado rápido escrito en Rust.
   - **`conform.nvim`**: Asignar formateadores automáticos por tipo de archivo (`prettier`, `stylua`, `shfmt`) ejecutados con `<space> + f`.
   - **`mini.pairs`**: Autocompletar comillas y paréntesis automáticamente.
   - **`gitsigns` + `mini.diff`**: Indicadores de líneas añadidas/modificadas en la columna lateral y atajos `gh` / `gH` / `]c` / `[c`.
   - **`todo-comments`**: Resaltado de etiquetas como `TODO:`, `FIXME:`, `NOTE:`.
3. **`lua/rvim/utils/lazygit.lua`**:
   - Integración para disparar `lazygit` mediante `;g` en una terminal flotante.

---

### 🔴 FASE 6: Inteligencia de Código (LSP) y Afinación Final
*Objetivo: Autocompletado contextual, tipos, errores y navegación semántica.*

1. **Añadir a `plugins/init.lua`**:
   ```lua
   { src = gh("neovim/nvim-lspconfig") },
   { src = gh("mason-org/mason.nvim") },
   { src = gh("WhoIsSethDaniel/mason-tool-installer.nvim") },
   ```
2. **`lua/rvim/plugins/lsp.lua`**:
   - Configurar `mason` para instalar automáticamente los servidores deseados (`vtsls`, `lua_ls`, `tailwindcss`, etc.).
   - Conectar las capacidades de autocompletado de `blink.cmp` con `lspconfig`.
3. **`after/lsp/` (Módulos por servidor)**:
   - Separar las configuraciones complejas de cada servidor en archivos individuales dentro de `after/lsp/` (ej. `vtsls.lua` para TypeScript o `lua_ls.lua` para Neovim APIs).
4. **Completar `lua/rvim/plugins/keymaps.lua`**:
   - `gd` -> Ir a definición.
   - `gr` -> Ver referencias.
   - `K` -> Documentación hover.
   - `<space> + ca` -> Acciones de código (*Code Actions*).
   - `<space> + cr` -> Renombrar variable en todo el proyecto (*Rename*).

---

## 🏆 Resultado Final
Siguiendo estos pasos, `rvim` tendrá la misma velocidad, modularidad y elegancia que la configuración de Craftzdog, pero con código 100% tuyo, comprendido y bajo tu propio control.
