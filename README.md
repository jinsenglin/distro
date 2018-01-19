REF http://www.frankreimer.de/?p=522

# Prepare a building machine

```
vagrant init bento/centos-7.2
vagrant up
vagrant ssh

sudo su
```

# Download a base distro

```
wget http://archive.kernel.org/centos-vault/7.2.1511/isos/x86_64/CentOS-7-x86_64-Minimal-1511.iso
```

# Mount the base distro

```
mkdir -p /mnt/iso
mount -o loop CentOS-7-x86_64-Minimal-1511.iso /mnt/iso
```
