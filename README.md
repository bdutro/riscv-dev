# RISC-V Development Environment

This repo manages a universal RISCV development environment based on Arch Linux

## Setup

For convenience, the environment is available as a Docker container, a Vagrant VM, or a VirtualBox appliance. **You only need to set it up with one of these methods.**

Docker requires the fewest system resources, while VirtualBox is the most user-friendly for people who are new to virtualization. The Vagrant VM is included for those who prefer it to Docker.

**Note:** Commands run on the host are prefixed with `$`. Commands run on the container/VM are prefixed with `$$`.

#### System Requirements

These images all require an x86_64 host machine with at least 4 cores and 8GB of RAM. All of the environments are limited to 4GB of RAM and the VMs are limited to 2 virtual CPUs.

### Docker

Install Docker using [these instructions](https://docs.docker.com/install/).

```
$ docker pull bdutro/riscv-dev
$ docker run -it --name riscv -v <path to local work directory>:/work -m 4g bdutro/riscv-dev /bin/bash
$$ exit
$ docker stop -t 0 riscv
```

### VirtualBox

1. Download the relevant VirtualBox installer for your system from [here](https://www.virtualbox.org/wiki/Downloads) and install using [these instructions](https://www.virtualbox.org/manual/ch02.html).
2. Download the latest `riscv-dev.ova` from the [Releases area](https://github.com/bdutro/riscv-dev/releases/) and import it into VirtualBox.

### Vagrant

Install Vagrant using [these instructions](https://www.vagrantup.com/docs/installation).

```
$ mkdir riscv-dev
$ cd riscv-dev
$ vagrant init bdutro/riscv-dev
$ vagrant up
$ vagrant ssh
$$ exit
$ vagrant halt
```

## Usage

### Starting the Environment

#### Docker

```
$ docker start riscv
$ docker exec -it riscv /bin/bash
```

#### VirtualBox

Start VirtualBox and run the `riscv-dev` VM. You can either interact through the VirtualBox GUI or connect via SSH.

Log in through the GUI (the username is **riscv** and the password is **riscv**), then run the following to get the IP address:

```
$$ ip addr show eth0 | grep 'inet '
    inet <ip-address>/24 ...
```

Once you have the IP you can SSH into the VM:
```
$ ssh riscv@<ip-address>
```

#### Vagrant

```
$ cd riscv-dev
$ vagrant up
$ vagrant ssh
```

### Compiling and Simulating a RISCV Program

There are 2 toolchains installed: baremetal (`riscv64-elf-*`) and Linux (`riscv64-linux-gnu-*`). The baremetal toolchain should be used when simulating on `spike`.

Suppose you want to compile and run a C program named main.c:

```
$$ riscv64-elf-gcc -o main main.c
$$ spike /usr/riscv64-linux-gnu/bin/pk main
```

### Stopping the Environment

#### Docker

```
$$ exit
$ docker stop -t 0 riscv
```

#### VirtualBox

```
$$ sudo poweroff
```

#### Vagrant

```
$$ exit
$ vagrant halt
```

## Acknowledgements

The VirtualBox images are built using a Packer template based on https://github.com/elasticdog/packer-arch
