# qiskit-sandbox



```bash
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

