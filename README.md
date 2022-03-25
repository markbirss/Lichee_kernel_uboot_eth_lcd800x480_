# Lichee_kernel_uboot_eth_lcd800x480_
Lichee Zero Pi with LCD 800x480 and ETH + (WIFI) support compiled files



```shell
# Install the cross-compile toolchain
# Download from:

https://licheepizero.us/arm-linux-gnueabihf/ (Mirror)
https://releases.linaro.org/components/toolchain/binaries/6.3-2017.05/arm-linux-gnueabihf/
# Use the following commands to install:

wget https://licheepizero.us/arm-linux-gnueabihf/gcc-linaro-6.3.1-2017.05-x86_64_arm-linux-gnueabihf.tar.xz
tar xvf gcc-linaro-6.3.1-2017.05-x86_64_arm-linux-gnueabihf.tar.xz
mv gcc-linaro-6.3.1-2017.05-x86_64_arm-linux-gnueabihf /opt/
vim /etc/bash.bashrc
add: PATH="$PATH:/opt/gcc-linaro-6.3.1-2017.05-x86_64_arm-linux-gnueabihf/bin"
arm-linux-gnueabihf-gcc -v
sudo apt-get install device-tree-compiler
```

```shell
# also remove if is installed arm-linux-gnueabihf-gcc by apt

sudo apt remove arm-linux-gnueabihf-gcc
```

# APPLY PATCH ON linux-5.12.zip (for ethernet support)

```shell
cd linux

cp ../licheepi-kernel-5.12.0.patch .
git apply licheepi-kernel-5.12.0.patch
```

```shell
# Linux => use rather linux-5.12.zip
# git clone https://github.com/Lichee-Pi/linux.git -b zero-4.13.y

CROSS_COMPILE=arm-linux-gnueabihf- ARCH=arm make licheepi_zero_defconfig
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- -j4
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- dtbs
```

```shell
# Uboot

git clone https://github.com/Lichee-Pi/u-boot.git -b v3s-current
ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- make LicheePi_Zero_800x480LCD_defconfig
ARCH=arm make menuconfig   
ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- make -j4
```

![Image description](https://github.com/nathalis/Lichee_kernel_uboot_eth_lcd800x480_/blob/main/Uboot%20ethernet%20enable/68747470733a2f2f626f782e6b616e636c6f75642e636e2f61343731386236363966386239626433646161373530643361353039356532365f393732783538322e706e67.png)


target files: 

```shell
zImage
u-boot-sunxi-with-spl.bin
sun8i-v3s-licheepi-zero-dock.dtb
rtl8xxxu.ko
```


![Image description](https://github.com/nathalis/Lichee_kernel_uboot_eth_lcd800x480_/blob/main/2022-03-25%20at%2019-38-34.jpg)


