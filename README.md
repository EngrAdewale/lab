
# 🐳 Kubernetes Setup Notes (Rancher Desktop + WSL + CLI Enhancements)

## 🖥️ Environment

- **Platform**: Rancher Desktop  
- **Shell**: WSL2 (Ubuntu)  
- **Editor**: Vim

---

## ⚙️ Bash Customization for `kubectl`

1. Open your `.bashrc` file:

   ```bash
   vim ~/.bashrc
   ```

2. Add the following block to configure `kubectl` aliases and autocomplete:

   ```bash
   # kubectl shortcuts and autocompletion
   alias k='kubectl'
   alias kgp='kubectl get pods'
   alias kc='kubectx'
   alias kn='kubens'

   source /etc/bash_completion
   source <(kubectl completion bash)
   complete -o default -F __start_kubectl k
   ```

3. Apply the changes:

   ```bash
   source ~/.bashrc
   ```

---

## ✍️ Vim Configuration for YAML/Kubernetes Files

In your `~/.vimrc` (or inside `.vimrc` section of `.bashrc`), add:

```vim
" Enable filetype-specific plugins and indentation
filetype plugin on
filetype indent on

" Set consistent 2-space indentation
set tabstop=2
set softtabstop=2
set shiftwidth=2
set expandtab

" Highlight trailing whitespace
autocmd BufRead,BufNewFile * match Error /\s\+$/

" Enable auto-indentation and syntax highlighting
set autoindent
syntax on

" Fix backspace behavior
set backspace=indent,eol,start
```

---

## 🚀 Install `kubectx` and `kubens` (Switch Clusters & Namespaces Easily)

### ✅ Step 1: Install Required Dependencies

```bash
sudo apt update
sudo apt install -y curl git bash-completion
```

### ✅ Step 2: Clone & Link `kubectx` and `kubens`

```bash
git clone https://github.com/ahmetb/kubectx ~/.kubectx
sudo ln -s ~/.kubectx/kubectx /usr/local/bin/kubectx
sudo ln -s ~/.kubectx/kubens /usr/local/bin/kubens
```

### ✅ Step 3: Enable Autocompletion

Add the following to your `~/.bashrc`:

```bash
# Autocompletion for kubectx and kubens
source ~/.kubectx/completion/kubectx.bash
source ~/.kubectx/completion/kubens.bash
```

Then reload your shell:

```bash
source ~/.bashrc
```

---

## 🧪 Usage Shortcuts

| Command   | Description                      |
|-----------|----------------------------------|
| `kubectx` | List & switch Kubernetes contexts |
| `kubens`  | List & switch namespaces         |
| `kc`      | Alias for `kubectx`              |
| `kn`      | Alias for `kubens`               |
| `kgp`     | Alias for `kubectl get pods`     |
| `k`       | Alias for `kubectl`              |

---

## 🗂️ WSL Tip: Access Windows Files from Ubuntu

Use the following command to navigate to your Windows user folder from WSL:

```bash
cd /mnt/c/Users/Owner
```

---

## 🧠 Conceptual Note

> **Kubernetes is the operating system of the cloud.**  
> It enables virtual machines and containers to communicate effectively and distribute workloads efficiently across environments.
