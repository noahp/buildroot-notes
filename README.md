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

I ran through menuconfig and set a few flags, in the savedefconfig output below.

But quicker option would be `make qemu_x86_64_defconfig` :grinning:

```defconfig
BR2_HAVE_DOT_CONFIG=y
BR2_i386=y
BR2_x86_i686=y
BR2_ARCH="i686"
BR2_ENDIAN="LITTLE"
BR2_GCC_TARGET_TUNE="i686"
BR2_GCC_TARGET_ARCH="i686"
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
qemu-system-x86_64 -nographic -append "console=ttyS0" -enable-kvm -kernel output/images/bzImage

# login is root, no password
```
