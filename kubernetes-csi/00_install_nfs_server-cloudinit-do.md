## cloud init to setup nfs 

```
#!/bin/bash 

groupadd sshadmin
USERS="11trainingdo $(echo tln{1..12})"
echo $USERS
for USER in $USERS
do
  echo "Adding user $USER"
  useradd -s /bin/bash $USER
  usermod -aG sshadmin $USER
  echo "$USER:somepasscomeshere" | chpasswd
  mkdir -p /var/nfs/tln{1..12}/nginx
done

# We can sudo with 11trainingdo
usermod -aG sudo 11trainingdo 

# Setup ssh stuff 
# 20.04 and 22.04 this will be in the subfolder
if [ -f /etc/ssh/sshd_config.d/50-cloud-init.conf ]
then
  sed -i "s/PasswordAuthentication no/PasswordAuthentication yes/g" /etc/ssh/sshd_config.d/50-cloud-init.conf
fi

## both is needed 
sed -i "s/PasswordAuthentication no/PasswordAuthentication yes/g" /etc/ssh/sshd_config



usermod -aG sshadmin root
echo "AllowGroups sshadmin" >> /etc/ssh/sshd_config 
systemctl reload sshd 

# update repo 
apt-get update 
apt-get install -y nfs-kernel-server

### Setup exports file 

### Show exports file 
echo '/var/nfs 10.135.0.0/24(rw,sync,no_root_squash,no_subtree_check)' >> /etc/exports;
exportfs -av
```
