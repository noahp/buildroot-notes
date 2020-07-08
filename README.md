# buildroot (x86-64 target)

How to buildroot!

## prerequisites

Assumes ubuntu/debian like host.

```bash
# build
sudo apt install -y build-essential

# running the built image
sudo apt install -y \
    bridge-utils \
    libvirt-clients \
    libvirt-daemon-system \
    qemu \
    qemu-kvm \
    virt-manager
```

## get buildroot

```bash
git clone git://git.buildroot.net/buildroot
```

## config

```defconfig
BR2_x86_64=y
BR2_KERNEL_HEADERS_5_7=y
BR2_LINUX_KERNEL=y
BR2_LINUX_KERNEL_USE_ARCH_DEFAULT_CONFIG=y
BR2_TARGET_ROOTFS_ISO9660=y
BR2_TARGET_SYSLINUX=y
```

Configure it using:

```bash
make defconfig BR2_DEFCONFIG=<path-to-defconfig-file>
```

## build

Takes about 10-15 minutes on my crummy laptop (https://www.amd.com/en/products/apu/amd-ryzen-3-2300u).
Note that you need internet during the build, buildroot fetches sources as it goes.

```bash
make --load-average=8
```

## test it!

```bash
qemu-system-x86_64 -cdrom output/images/rootfs.iso9660

# login is root, no password
```
