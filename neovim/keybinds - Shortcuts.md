## Plugin: `telescope.nvim`

| Shortcut | Action                  |
| -------- | ----------------------- |
| `SPC` ff | Find file               |
| `SPC` fg | Live grep (search text) |
| `SPC` fb | List open buffers       |
| `SPC` fh | Help tags (search help) |
| `SPC` fo | Recently opened files   |
## Plugin: `tab management` (built-in)

| Shortcut | Action             |
| -------- | ------------------ |
| SPC to   | Open new tab       |
| SPC tx   | Close current tab  |
| SPC tn   | Go to next tab     |
| SPC tp   | Go to previous tab |

## **Plugin:** `comment.nvim`

| Shortcut      | Action                             |
| ------------- | ---------------------------------- |
| `gcc`         | Toggle comment on the current line |
| `gc` + motion | Toggle comment on selected lines   |
Examples:
- `gc3j` → Comments 3 lines down
- `gcip` → Comments current paragraph

## **Plugin:** `which-key.nvim`
| Shortcut  | Action                                                                            |
| --------- | --------------------------------------------------------------------------------- |
| `<Space>` | Opens a popup showing available keybindings based on the current mode and context |
Note: You don’t trigger specific actions directly with `which-key`; it acts as a **guide layer** to display all mappings bound under prefixes like `SPC`, `g`, `z`, etc.


## **Plugin:** `lspconfig` (via `mason-lspconfig` and `nvim-lspconfig`)
| Shortcut     | Action                                  |
| ------------ | --------------------------------------- |
| `K`          | Show hover documentation                |
| `<leader>dn` | Go to next diagnostic message           |
| `<leader>dp` | Go to previous diagnostic message       |
| `:LspInfo`   | Show active LSP servers and status      |
| `:Mason`     | Open Mason UI to install/manage servers |
## **Plugin:** `conform.nvim` (code formatter)

| Shortcut     | Action                                                  |
| ------------ | ------------------------------------------------------- |
| `:Format`    | Manually format the current buffer                      |
| `(autosave)` | Automatically formats on save (if enabled per language) |
Note: Formatting behavior depends on the filetype and the formatter installed (e.g., `black` for Python, `prettier` for JS).


## **Plugin:** `nvim-cmp` (Autocompletion engine)

|Shortcut|Action|
|---|---|
|(no explicit keybinds set manually)|Autocompletion triggers automatically while typing|
|`<Tab>` / `<Shift-Tab>`|Navigate through completion items|
|`<CR>` (Enter)|Confirm selected completion item|
Note: These mappings are usually provided internally by the plugin unless overridden. You can later customize them for your preferences.

## General Keymaps

| Shortcut    | Action                                  |
| ----------- | --------------------------------------- |
| `jk`        | Exit insert mode                        |
| `<leader>w` | Save file                               |
| `<leader>q` | Quit                                    |
| `<leader>h` | Clear search highlights (`:nohlsearch`) |
| `<leader>+` | Increment number under cursor           |
| `<leader>-` | Decrement number under cursor           |

## **Window Management**

| Shortcut     | Action                               |
| ------------ | ------------------------------------ |
| `<leader>sv` | Split window vertically (`<C-w>v`)   |
| `<leader>sh` | Split window horizontally (`<C-w>s`) |
| `<leader>se` | Make splits equal width (`<C-w>=`)   |
| `<leader>sx` | Close current split window           |

## Tab Management
| Shortcut     | Action             |
| ------------ | ------------------ |
| `<leader>to` | Open new tab       |
| `<leader>tx` | Close current tab  |
| `<leader>tn` | Go to next tab     |
| `<leader>tp` | Go to previous tab |
## **Telescope (Plugin-Related)**

| Shortcut     | Action                   |
| ------------ | ------------------------ |
| `<leader>ff` | Find files (`Telescope`) |
| `<leader>fg` | Live grep (`Telescope`)  |
**Flash.nvim (Fast Navigation)**

| Shortcut    | Action     |
| ----------- | ---------- |
| `<leader>s` | Flash jump |
:


Copy Mode

| Action    | Keybinding              |
| --------- | ----------------------- |
| Space + y | In copy mode: press `v` |
