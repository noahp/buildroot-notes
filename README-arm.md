# buildroot (arm target)

## prerequisites

Same prereqs, plus:

```bash
# qemu for arm
sudo apt install -y qemu-system-arm
```

## config + build

```bash
make qemu_arm_versatile_defconfig
make --load-average=8
```

## test

From https://dzone.com/articles/an-arm-image-with-buildroot .

```bash
qemu-system-arm \
    -M versatilepb \
    -kernel output/images/zImage \
    -dtb output/images/versatile-pb.dtb \
    -drive file=output/images/rootfs.ext2,if=scsi,format=raw \
    -append "root=/dev/sda console=ttyAMA0,115200" \
    -serial stdio \
    -net nic,model=rtl8139 \
    -net user \
    -name Versatile_ARM_EXT2
```
