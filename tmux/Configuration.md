## Folder & File Structure
~/
├── .tmux.conf                 # Main configuration file
└── .tmux/
    └── plugins/
        └── tpm/               # Tmux Plugin Manager (TPM) cloned here
## Full `.tmux.conf` Configuration

```bash
# Prefix key: Ctrl + s
set -g prefix C-s

# Terminal compatibility
set -g default-terminal "screen-256color"
set -ga terminal-overrides ',xterm-256color:Tc'

# Enable mouse support
set -g mouse on

# Performance & usability tweaks
set -gq allow-passthrough on
set -g visual-activity off
set -g base-index 1
set -sg escape-time 0

# Reload config shortcut
bind r source-file ~/.tmux.conf \; display-message "config reloaded"

# Vim-style pane navigation
setw -g mode-keys vi
bind-key h select-pane -L
bind-key j select-pane -D
bind-key k select-pane -U
bind-key l select-pane -R

# Vim-style copy mode
bind-key -T copy-mode-vi 'v' send -X begin-selection
bind-key -T copy-mode-vi 'y' send -X copy-selection-and-cancel

# Status bar appearance
set-option -g status-position top   # Change to 'bottom' if you prefer
set -g status-right '#[fg=color249]#(date +"%I:%M%p %m-%d-%Y")#[default]'

# Status bar styling
set-option -g status-bg color233
set-option -g status-fg color249
set -g mode-style "fg=color0,bg=color11"
set -g pane-active-border-style 'fg=color238'
set -g pane-border-style 'fg=color236'

# Extra keybindings
bind C-j display-popup -E "list-sessions | sed -E 's/:.*$//' | grep -v \"^$(display-message -p '#S')\$\" | fzf --reverse | xargs switch-client -t"
bind d detach
bind-key C-n command-prompt -p "New session name:" "new-session -s '%%'"

# Plugin definitions
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-resurrect'
set -g @plugin 'tmux-plugins/tmux-continuuk'
set -g @plugin 'christoomey/vim-tmux-navigator'

# Initialize TPM
run '~/.tmux/plugins/tpm/tpm'
```
## Commands to Set It Up (one-time)
``` bash
# Install tmux
sudo apt install tmux -y

# Create .tmux.conf and paste config
nano ~/.tmux.conf

# Clone TPM (Tmux Plugin Manager)
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm

# Launch tmux and press: Ctrl + s, then I (capital i) to install plugins
tmux
```
