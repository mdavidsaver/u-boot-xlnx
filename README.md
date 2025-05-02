# u-boot for picozed and BNL/LBL PSC

See upstream u-boot [README](README).

## Build u-boot

On Debian 12.

```sh
sudo apt-get install libssl-dev uuid-dev libgnutls-dev \
  binutils-arm-linux-gnueabi \
  g++-arm-linux-gnueabihf \
  libc6-dev-armel-cross
```

```
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- \
  distclean

make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- \
  xilinx_zynq_picozed_psc_defconfig

make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- \
  all
```

## Assembly BOOT.bin

To create a bootable image, the resulting `u-boot.elf`
needs to be combined with an `fsbl.elf` from a Vitis
project using the `bootgen` tool.

```sh
cat <<EOF > u-boot.bif
u_boot:
{
        [bootloader]fsbl.elf
        u-boot.elf
}
EOF

bootgen -arch zynq -image u-boot.bif -w -o BOOT.bin
```

## TODO

`./tools/mkenvimage` to create `uboot.env`
