REF http://www.frankreimer.de/?p=522

Steps

* Prepare a building machine
* Download a base distro
* Mount the base distro
* Create a working directory
* Copy needed content from base distro to working directory
* Copy packages and create repodata
* Prepare kickstart file
* Create a custom distro ISO file
* Verify installation by kickstart file

---

# Prepare a kickstart file

```
touch ~/kickstart_build/isolinux/ks/ks.cfg

# Hint: lazy way is `cp anaconda-ks.cfg ~/kickstart_build/isolinux/ks/ks.cfg`
```

---

# Verify installation by the kickstart file

```
# Now start a new virtual machine from your custom distro ISO file and insert the following option at kernel boot:

linux inst.ks=cdrom:/dev/cdrom:/ks/ks.cfg

# Hint: in boot menu type `esc` two times to enter boot mode prompter
```
