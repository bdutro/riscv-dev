FROM archlinux:base-devel

RUN pacman -Syu --noconfirm
RUN pacman -S --noconfirm riscv32-elf-binutils riscv32-elf-gdb riscv32-elf-newlib riscv64-elf-binutils riscv64-elf-gcc riscv64-elf-gdb riscv64-elf-newlib riscv64-linux-gnu-binutils riscv64-linux-gnu-gcc riscv64-linux-gnu-gdb riscv64-linux-gnu-glibc riscv64-linux-gnu-linux-api-headers spike git nano vim emacs
RUN useradd --shell=/bin/bash riscv
USER riscv
RUN cd /tmp && git clone https://aur.archlinux.org/riscv-pk.git && cd riscv-pk && makepkg
USER root
RUN pacman -U --noconfirm /tmp/riscv-pk/riscv-pk-*-x86_64.pkg.tar.zst
RUN mkdir /work && chown -R riscv:riscv /work
USER riscv
