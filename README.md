REF http://www.frankreimer.de/?p=522

# Prepare a building machine

```
vagrant init bento/centos-7.2 --box-version 2.3.1
vagrant up
vagrant ssh

sudo su
yum install -y rsync createrepo genisoimage
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
cp /mnt/iso/.discinfo ~/kickstart_build/isolinux/

cp /mnt/iso/isolinux/* ~/kickstart_build/isolinux/

rsync -av /mnt/iso/images/ ~/kickstart_build/isolinux/images/

cp /mnt/iso/LiveOS/* ~/kickstart_build/isolinux/LiveOS/

ll /mnt/iso/repodata/ | grep -i c7-minimal-x86_64-comps.xml.gz
-r--r--r--. 1 root root   3663 Dec  9  2015 4a04a16ba51071ab8942bc507087ed59cac82e9b22134b322f1452a45b87a1a2-c7-minimal-x86_64-comps.xml.gz

cp /mnt/iso/repodata/4a04a16ba51071ab8942bc507087ed59cac82e9b22134b322f1452a45b87a1a2-c7-minimal-x86_64-comps.xml.gz ~/kickstart_build/

cd ~/kickstart_build/
gunzip 4a04a16ba51071ab8942bc507087ed59cac82e9b22134b322f1452a45b87a1a2-c7-minimal-x86_64-comps.xml.gz
mv 4a04a16ba51071ab8942bc507087ed59cac82e9b22134b322f1452a45b87a1a2-c7-minimal-x86_64-comps.xml comps.xml
```

# Copy packages and create repodata

```
rsync -av /mnt/iso/Packages/ ~/kickstart_build/isolinux/Packages/

cd ~/kickstart_build/isolinux
createrepo -g ~/kickstart_build/comps.xml .
```

# Create a custom distro ISO file

```
cd ~/kickstart_build/
mkisofs -o centos-7-custom.iso -b isolinux.bin -c boot.cat -no-emul-boot -V 'CentOS 7 x86_64' -boot-load-size 4 -boot-info-table -R -J -v -T isolinux/

# output file: ~/kickstart_build/centos-7-custom.iso
```

# Additional Resources

Anaconda is the installer used by Red Hat Enterprise Linux, Fedora, and their derivatives. This document contains information necessary for customizing it. https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html-single/anaconda_customization_guide/index
