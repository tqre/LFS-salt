# Linux From Scratch & Saltstack
## saltminion in vagrantbox

This project is based on Linux From Scratch 8.4-systemd, which has to compiled succesfully first. 
If you really want to learn what makes Linux tick, this is where to head:
http://www.linuxfromscratch.org/lfs/view/8.4-systemd/

Beyond Linux From Scratch guide is used to compile the tools needed:

http://www.linuxfromscratch.org/blfs/view/8.4-systemd/

I have removed the original Linux used for compiling and configured network connection with systemd.

### Steps to make Linux From Scratch Vagrant box:
- compile wget
- install BLFS systemd units
- compile openSSH
- compile sudo
- make vagrant user
- give vagrant user sudo rights
- set up the insecure keys from vagrant
- enable sshd
- virtualbox nat
- Vagrantfile tuning, no synced folders
- minimize the resources on the virtual machine before packaging the box
  - 128MB Ram, no audio, no usb, poiniting device PS/2 Mouse, minimal video memory (9MB)
- package the box
  
### Steps to compile Saltstack on LFS:
- download dependencies (salt/saltdeps)
- download salt source (2019.2.0) & install
- tornado version 6 breaks the build, use 5.1.1 instead
- compiling scripts pending
  - python3 setup.py build
  - python3 setup.py install
- for ZeroMQ & yaml:
  - ./configure --prefix=/usr
  - make
  - make install
- make systemd service file
  - https://github.com/saltstack/salt/blob/develop/pkg/salt-minion.service

- make minion config file /etc/salt/minion
- enable salt-minion.service

### Current progress
Manually created working salt-LFS version, where archlive-master can see and command LFS-salt-minion
in virtualbox created NAT Network. Works despite master having a different Python version.
Vagrantbox is ssh'able.

Recompiled libffi and libgmp for generic architectures as testing laptop had AMD-processor.

Salt-minion.service working!
