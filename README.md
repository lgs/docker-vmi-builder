## Docker VMI Builder

  [docker-vmi-builder](http://github.com/cmfatih/docker-vmi-builder) is a [Docker](http://www.docker.io/) virtual machine image builder for Ubuntu. 
  The VMI file can be used with any virtual machine which has support for x86_64 / amd64 system and qcow2 disk image format.
  
### Installation

```
git clone https://github.com/cmfatih/docker-vmi-builder.git
```

### Usage

```
./docker-vmi-builder.sh
```

### Test

```
sudo qemu-system-x86_64 -m 512 -hda docker-vmi-img.img -display none -usbdevice tablet -vnc :5,docker -net user,hostfwd=tcp:127.0.0.1:8022-:22 -net nic -daemonize
ssh dockervmi@127.0.0.1 -p 8022
```

### Requirements

```
Ubuntu Packages
  qemu-system 
  rsync 
  genisoimage
```

### Notes

* For login; username: `dockervmi` , password: `dockervmi`
* The building process requires *sudo* for mounting Ubuntu ISO file.
* *ubuntu-12.04.3-server-amd64.iso* file (697MB) will be downloaded from Ubuntu server. Putting this file to the script folder (before running the builder) will prevent download process.
* The process will create ~1.33GB **uncompressed** qcow2 formatted image file. It can be **compress** to ~500MB.
* The building process takes ~15 minutes with AMD 12 core CPU, 32GB RAM, SSD disk. It can be monitor with VNC client.
* Qemu doesn't require X Window System. Use `-display none -net user,hostfwd=tcp:127.0.0.1:8022-:22 -net nic` parameter for starting VM and use `ssh dockervmi@127.0.0.1 -p 8022` for connection.
* [Qemu for Windows](http://lassauge.free.fr/qemu/) doesn't require any installation. So [Qemu archive file](http://lassauge.free.fr/qemu/release/Qemu-1.5.1-windows.zip) and the VMI can be contribute with a single archive file.

### Changelog

* 20130929 `-enable-kvm` option is removed. The login username and password changed.
* 20130919 Ubuntu 12.04.3 and Docker v0.6.x (Docker repository)

### Showcase

**The building process**

![docker-vmi-builder.sh](docs/img/dvb-out.png)

**Using the VMI on Windows with Qemu+SSH+PuTTY**

![docker-vmi-img.img](docs/img/vmi-win-qemu-ssh.png)

### License

Copyright (c) 2013 Fatih Cetinkaya (http://github.com/cmfatih/docker-vmi-builder)  
Licensed under The MIT License (MIT)  
For the full copyright and license information, please view the LICENSE.txt file.
