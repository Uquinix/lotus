Spike Simulator Platform
========================

The **Spike** is a RISC-V ISA simulator which implements a functional model
of one or more RISC-V harts. The **Spike** compatible virtual platform is
also available on QEMU. In fact, we can use same OpenSBI firmware binaries
on **Spike** simulator and QEMU Spike machine.

For more details, refer [Spike on GitHub](https://github.com/riscv/riscv-isa-sim)

To build the platform-specific library and firmware images, provide the
*PLATFORM=generic* parameter to the top level `make` command.

Platform Options
----------------

The *Spike* platform does not have any platform-specific options.

Execution on Spike Simulator
----------------------------

**No Payload Case**

Build:
```
make PLATFORM=generic
```

Run:
```
spike build/platform/generic/firmware/fw_payload.elf
```

**Linux Kernel Payload**

Note: We assume that the Linux kernel is compiled using
*arch/riscv/configs/defconfig*.

Build:
```
make PLATFORM=generic FW_PAYLOAD_PATH=<linux_build_directory>/arch/riscv/boot/Image
```

Run:
```
spike -m256 \
	--initrd <path_to_cpio_ramdisk> \
	--bootargs 'root=/dev/ram rw console=hvc0 earlycon=sbi' \
	build/platform/generic/firmware/fw_payload.elf
```
or
```
spike -m256 \
	--kernel <linux_build_directory>/arch/riscv/boot/Image \
	--initrd <path_to_cpio_ramdisk> \
	--bootargs 'root=/dev/ram rw console=hvc0 earlycon=sbi' \
	build/platform/generic/firmware/fw_jump.elf
```

Execution on QEMU RISC-V 64-bit
-------------------------------

**No Payload Case**

Build:
```
make PLATFORM=generic
```

Run:
```
lotus-system-riscv64 -M spike -m 256M -nographic \
	-bios build/platform/generic/firmware/fw_payload.elf
```

**Linux Kernel Payload**

Note: We assume that the Linux kernel is compiled using
*arch/riscv/configs/defconfig*.

Build:
```
make PLATFORM=generic FW_PAYLOAD_PATH=<linux_build_directory>/arch/riscv/boot/Image
```

Run:
```
lotus-system-riscv64 -M spike -m 256M -nographic \
	-bios build/platform/generic/firmware/fw_payload.elf \
	-initrd <path_to_cpio_ramdisk> \
	-append "root=/dev/ram rw console=hvc0 earlycon=sbi"
```
or
```
lotus-system-riscv64 -M spike -m 256M -nographic \
	-bios build/platform/generic/firmware/fw_jump.elf \
	-kernel <linux_build_directory>/arch/riscv/boot/Image \
	-initrd <path_to_cpio_ramdisk> \
	-append "root=/dev/ram rw console=hvc0 earlycon=sbi"
```
