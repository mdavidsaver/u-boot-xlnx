# u-boot for picozed and BNL/LBL PSC

See upstream u-boot [README](README).

## Build

On Debian 12.

```sh
sudo apt-get install \
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

Output products are:

- `spl/boot.bin` Copy to SD card as `BOOT.bin`.
- `u-boot.img` Copy to SD card.

## TODO

`./tools/mkenvimage` to create `uboot.env`
