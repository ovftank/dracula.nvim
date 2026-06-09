<h1 align="center" >🧛‍♂️ ovftank/dracula</h1>

<p align="center"><a href="https://draculatheme.com/">Dracula</a> colorscheme for <a href="https://neovim.io/">NEOVIM</a> written in Lua</p>

![ovftank/dracula](./assets/showcase.png)

## ✔️ Requirements

- Neovim >= 0.9.2
- Treesitter (optional)

This fork keeps the original MIT license notice and focuses on matching the official VS Code Dracula colors more closely in Neovim-native highlight groups.

## #️ Supported Plugins

- [LSP](https://github.com/neovim/nvim-lspconfig)
- [Treesitter](https://github.com/nvim-treesitter/nvim-treesitter)
- [nvim-compe](https://github.com/hrsh7th/nvim-compe)
- [nvim-cmp](https://github.com/hrsh7th/nvim-cmp)
- [blink.cmp](https://github.com/Saghen/blink.cmp/)
- [Telescope](https://github.com/nvim-telescope/telescope.nvim)
- [NvimTree](https://github.com/kyazdani42/nvim-tree.lua)
- [NeoTree](https://github.com/nvim-neo-tree/neo-tree.nvim)
- [BufferLine](https://github.com/akinsho/nvim-bufferline.lua)
- [Git Signs](https://github.com/lewis6991/gitsigns.nvim)
- [Lualine](https://github.com/hoob3rt/lualine.nvim)
- [LSPSaga](https://github.com/glepnir/lspsaga.nvim)
- [indent-blankline](https://github.com/lukas-reineke/indent-blankline.nvim)
- [nvim-ts-rainbow](https://github.com/p00f/nvim-ts-rainbow)
- [nvim-dap-ui](https://github.com/rcarriga/nvim-dap-ui)
- [mini.indentcope](https://github.com/echasnovski/mini.indentcope)
- [mini.icons](https://github.com/echasnovski/mini.icons)
- [mini.statusline](https://github.com/echasnovski/mini.statusline)

## ⬇️ Installation

### lazy.nvim

```lua
{
  "ovftank/dracula",
  lazy = false,
  priority = 1000,
  opts = {},
  config = function(_, opts)
    require("dracula").setup(opts)
    vim.cmd.colorscheme("dracula")
  end,
}
```

Use `lazy = false` when this is your main colorscheme so it is available during startup. `priority = 1000` makes the theme load before other start plugins that define highlights.

### packer.nvim

```lua
use "ovftank/dracula"
```

### vim-plug

```vim
Plug 'ovftank/dracula'
```

## 🚀 Usage

```lua
-- Lua:
vim.cmd[[colorscheme dracula]]
```

```vim
" Vim-Script:
colorscheme dracula
```

With lazy.nvim, prefer loading the colorscheme in the plugin spec `config` function shown above. That guarantees `setup()` runs before `:colorscheme dracula`.

If you want lazy.nvim to load the theme only when `:colorscheme dracula` is called, use:

```lua
{
  "ovftank/dracula",
  lazy = true,
}
```

This is useful when `dracula` is installed but not your startup colorscheme.

If you are using [`lualine`](https://github.com/hoob3rt/lualine.nvim), you can also enable the provided theme:

> Make sure to set theme as 'dracula-nvim' as dracula already exists in lualine built in themes

```lua
require('lualine').setup {
  options = {
    -- ...
    theme = 'dracula-nvim'
    -- ...
  }
}
```

If you are using [LazyVim](https://github.com/LazyVim/LazyVim), you can add this to your plugins/colorscheme.lua file:

```lua
return {
  -- add dracula
  { "ovftank/dracula" },

  -- Configure LazyVim to load dracula
  {
    "LazyVim/LazyVim",
    opts = {
      colorscheme = "dracula",
    },
  },
}
```

## How loading works

Neovim loads a colorscheme with `:colorscheme dracula` by searching for `colors/dracula.lua` in `runtimepath` and package paths. This file then calls `require("dracula").load()`.

The Lua module lives under `lua/dracula/`, so `require("dracula")` loads `lua/dracula/init.lua`. Neovim caches required Lua modules, so run `require("dracula").setup(...)` before `vim.cmd.colorscheme("dracula")`.

lazy.nvim takes over plugin startup and does not rely on Neovim's native package loading. For a startup colorscheme, use `lazy = false` and `priority = 1000`. For an optional colorscheme, `lazy = true` is fine because lazy.nvim can load colorscheme plugins when `:colorscheme dracula` is executed.

## 🔧 Configuration

The configuration must be run before `colorscheme` command to take effect.

Minimal lazy.nvim setup:

```lua
{
  "ovftank/dracula",
  lazy = false,
  priority = 1000,
  opts = {
    transparent_bg = false,
    italic_comment = false,
  },
  config = function(_, opts)
    require("dracula").setup(opts)
    vim.cmd.colorscheme("dracula")
  end,
}
```

If you're using Lua:

```lua
local dracula = require("dracula")
dracula.setup({
  -- customize dracula color palette
  colors = {
    bg = "#282A36",
    fg = "#F8F8F2",
    selection = "#44475A",
    comment = "#6272A4",
    red = "#FF5555",
    orange = "#FFB86C",
    yellow = "#F1FA8C",
    green = "#50FA7B",
    purple = "#BD93F9",
    cyan = "#8BE9FD",
    pink = "#FF79C6",
    bright_red = "#FF6E6E",
    bright_green = "#69FF94",
    bright_yellow = "#FFFFA5",
    bright_blue = "#D6ACFF",
    bright_magenta = "#FF92DF",
    bright_cyan = "#A4FFFF",
    bright_white = "#FFFFFF",
    ansi_black = "#21222C",
    ansi_white = "#F8F8F2",
    ansi_bright_black = "#6272A4",
    white_bright = "#FFFFFF",
    bg_dark = "#21222C",
    bg_darker = "#191A21",
    menu = "#21222C",
    visual = "#44475A",
    gutter_fg = "#6272A4",
    nontext = "#3E404A",
    white = "#ABB2BF",
    black = "#191A21",
  },
  -- show the '~' characters after the end of buffers
  show_end_of_buffer = true, -- default false
  -- use transparent background
  transparent_bg = true, -- default false
  -- set custom lualine background color
  lualine_bg_color = "#44475a", -- default nil
  -- set italic comment
  italic_comment = true, -- default false
  -- overrides the default highlights with table see `:h synIDattr`
  overrides = {},
  -- You can use overrides as table like this
  -- overrides = {
  --   NonText = { fg = "white" }, -- set NonText fg to white
  --   NvimTreeIndentMarker = { link = "NonText" }, -- link to NonText highlight
  --   Nothing = {} -- clear highlight of Nothing
  -- },
  -- Or you can also use it like a function to get color from theme
  -- overrides = function (colors)
  --   return {
  --     NonText = { fg = colors.white }, -- set NonText fg to white of theme
  --   }
  -- end,
})
```

## 🎨 Importing colors for other usage

```lua
local colors = require('dracula').colors()
```

This will return the following table (`dracula` palette shown):

![colors](./assets/colors.png)

## License

MIT. This fork keeps the original copyright and permission notice in `LICENSE.md`, as required by the MIT license.
