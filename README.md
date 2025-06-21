
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
# 📘 Kubernetes Architecture & Essential Commands

## 🧩 Kubernetes Control Plane Components

| Component     | Description |
|---------------|-------------|
| **API Server** (`kube-apiserver`) | Front-end of the control plane. Validates and processes kubectl/API requests. |
| **Scheduler** (`kube-scheduler`) | Assigns newly created pods to appropriate nodes based on resources and policies. |
| **etcd** | Distributed key-value store holding all cluster state (pods, secrets, services, etc.). |

---

## ⚙️ Common `kubectl` Commands

### 🔍 View Full Pod Configuration
```bash
k get pod <pod-name> -o yaml | less
```
- View the full YAML configuration of a running pod.
- `| less` enables page-by-page navigation in terminal.

---

### ✏️ Edit a Pod Live
```bash
k edit pod <pod-name>
```
- Opens the pod’s YAML in your default CLI editor for real-time editing.
- Use for quick tweaks or debugging.

---

### 🛠️ Generate Pod YAML from Command
```bash
k run nginx --image=nginx --dry-run=client -o yaml > nginx.yaml
```
- Simulates pod creation without deploying it (`--dry-run=client`).
- Saves the generated YAML into `nginx.yaml`.

---

### 🚀 Apply Configuration from YAML
```bash
k apply -f nginx.yaml
```
- Creates or updates Kubernetes resources from the YAML file.

---

### ✨ Vim Paste Mode (Optional)
```bash
:set paste
```
- In Vim, this avoids auto-indentation issues when pasting YAML or commands.

---

### 🌐 Get Pod Node and IP Info
```bash
k get pod -o wide
```
- Shows extra details like node name, IP address, and image used by the pod.

---

### 📦 Create a Deployment with Replicas
```bash
k create deploy test --image=httpd --replicas=3
```
- Deploys the `httpd` (Apache) image with 3 replicas under the name `test`.

---

### 📋 View Deployments
```bash
k get deployment.apps
```
- Lists all deployments in the current namespace.

