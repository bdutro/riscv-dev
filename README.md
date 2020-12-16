# RISCV Development Environment

This repo manages a universal RISCV development environment based on Arch Linux

## Setup

The environment is available as a Docker container or VM.

**Note**: Commands run on the host are prefixed with `$`. Commands run on the container/VM are prefixed with `$$`.

### Docker

Docker is a low-overhead virtualization engine that uses containers.

```
$ docker pull bdutro/riscv-dev
$ docker run -it --name riscv -v <path to local work directory>:/work -m 4g bdutro/riscv-dev /bin/bash
$$ exit
$ docker stop -t 0 riscv
```

### Vagrant

Vagrant is similar in some ways to Docker. The main difference is that it runs workloads in virtual machines instead of containers.

```
$ vagrant init bdutro/riscv-dev
$ vagrant up
$ vagrant ssh
$$ exit
$ vagrant halt
```

### VirtualBox

## Usage

### Starting the Environment

#### Docker

```
$ docker start riscv
$ docker exec -it riscv /bin/bash
```

#### Vagrant

```
$ vagrant up
$ vagrant ssh
```

#### VirtualBox

```
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

#### Vagrant

```
$$ exit
$ vagrant halt
```

#### VirtualBox

```
```
