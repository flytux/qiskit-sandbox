# qiskit-sandbox

### 1. Create k8sadm user, install docker, install k3s, set shell environment

```bash
groupadd -g 2000 k8sadm
useradd -m -u 2000 -g 2000 -s /bin/bash k8sadm
echo -e "1\n1" | passwd k8sadm >/dev/null 2>&1
echo ' k8sadm ALL=(ALL)   ALL' >> /etc/sudoers

apt update && apt install docker.io -y
usermod -aG docker k8sadm

curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION=v1.21.10+k3s1 sh -s - --docker --write-kubeconfig-mode 644

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod 755 kubectl && sudo mv kubectl /usr/local/bin
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

cat <<EOF >> ~/.bashrc
# k8s alias
source <(kubectl completion bash)
complete -o default -F __start_kubectl k
alias k=kubectl
alias vi=vim
alias kn='kubectl config set-context --current --namespace'
alias kc='kubectl config use-context'
alias kcg='kubectl config get-contexts'
alias di='docker images --format "table {{.Repository}}:{{.Tag}}\t{{.ID}}\t{{.Size}}\t{{.CreatedSince}}"'
EOF

source ~/.bashrc
```

