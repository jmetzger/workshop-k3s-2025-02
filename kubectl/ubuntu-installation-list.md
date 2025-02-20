# Ubuntu Installation List 

```
###########################################
# Phase 1: Install bash completion 
###########################################

apt-get update 
apt-get install -y bash-completion
source /usr/share/bash-completion/bash_completion
# is it installed properly
type _init_completion

###########################################
# Phase 2: Install kubectl  
# - install   kubectl - binary
# - configure kubectl - completion  
###########################################

echo "Installing kubectl"
snap install --classic kubectl
kubectl completion bash | sudo tee /etc/bash_completion.d/kubectl > /dev/null

###########################################
# Phase 3: Install helm & helm completion
# - install   helm - binary
# - configure helm - completion 
###########################################

echo "Installing helm"
snap install --classic helm 
helm completion bash | sudo tee /etc/bash_completion.d/helm > /dev/null

# Install nfs-common for mounting, just in case we need it for persistant storage exercise 
apt-get install -y nfs-common

# Looks like it takes a while till ssh is running 
date > /var/log/training_reload_ssh
systemctl restart ssh 

####################################
# Phase 4: Install k9s             
####################################

cd /usr/src 
wget https://github.com/derailed/k9s/releases/download/v0.32.5/k9s_linux_amd64.deb
dpkg -i k9s_linux_amd64.deb

###################################
# Phase 5: Install stern           
###################################

cd /usr/src
wget https://github.com/stern/stern/releases/download/v1.31.0/stern_1.31.0_linux_amd64.tar.gz
tar xvf stern_1.31.0_linux_amd64.tar.gz
install stern /usr/local/bin

###################################
# Phase 6: Install calicoctl      
###################################

cd /usr/local/bin
curl -L https://github.com/projectcalico/calico/releases/download/v3.28.2/calicoctl-linux-amd64 -o calicoctl
chmod +x ./calicoctl

###################################
# Phase 7: Configure vi  
###################################

# Activate syntax - stuff for vim
# Tested on Ubuntu 
echo "hi CursorColumn cterm=NONE ctermbg=lightred ctermfg=white" >> /etc/vim/vimrc.local 
echo "autocmd FileType y?ml setlocal ts=2 sts=2 sw=2 ai number expandtab cursorline cursorcolumn" >> /etc/vim/vimrc.local 
echo "set paste" >> /etc/vim/vimrc.local

###################################
# Phase 8: Configure - nano 
###################################

echo "include /usr/share/nano/yaml.nanorc" >> /etc/nanorc 
echo "set autoindent" >> /etc/nanorc
echo "set tabsize 2" >> /etc/nanorc
echo "set tabstospaces" >> /etc/nanorc 
```
