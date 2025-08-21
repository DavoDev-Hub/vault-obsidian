## LSP Setup (Language Server Protocol)
Language Server Protocol is configured to provide real-time feedback like:

- Syntax errors
- Warnings
- Type checks
- Code actions
- Hover documentation
- Autocompletion (via `nvim-cmp`)
## **Main components used:**
- `mason.nvim`: Installs and manages LSP servers.
- `mason-lspconfig.nvim`: Automatically bridges Mason with `nvim-lspconfig`.
- `nvim-lspconfig`: Configures and attaches LSP servers to relevant filetypes.

## **Installed LSP servers:**
- `pyright` for Python
- Others like `tsserver`, `lua_ls` can be added as needed.
