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

# Create a working directory

```
mkdir -p ~/kickstart_build/isolinux/{images,ks,LiveOS,Packages,postinstall}
```

# Copy needed content from base distro to working directory

```
rsync -a --exclude=Packages/ --exclude=repodata/ /mnt/cdrom/ /iso/
```

OR

```
cp /mnt/iso/.discinfo ~/kickstart_build/isolinux/

cp /mnt/iso/isolinux/* ~/kickstart_build/isolinux/

rsync -av /mnt/iso/images/ ~/kickstart_build/isolinux/images/

cp /mnt/iso/LiveOS/* ~/kickstart_build/isolinux/LiveOS/

ll /mnt/iso/repodata/ | grep -i comps
-rw-r--r--. 1 root root 157580 1. Apr 01:43 0e6e90965f55146ba5025ea450f822d1bb0267d0299ef64dd4365825e6bad995-c7-x86_64-comps.xml.gz

cp /mnt/iso/repodata/0e6e90965f55146ba5025ea450f822d1bb0267d0299ef64dd4365825e6bad995-c7-x86_64-comps.xml.gz ~/kickstart_build/

cd ~/kickstart_build/
gunzip 0e6e90965f55146ba5025ea450f822d1bb0267d0299ef64dd4365825e6bad995-c7-x86_64-comps.xml
mv 0e6e90965f55146ba5025ea450f822d1bb0267d0299ef64dd4365825e6bad995-c7-x86_64-comps.xml comps.xml
```
