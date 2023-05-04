Advantech RK3399 bsp Repo Manifest README
This repo is used to download manifests for Advantech RK3399 bsp releases.
## **Supported boards**
RK3399 Series
## Host PC Requirements
To use this manifest repo, the 'repo' tool must be installed first.
```
$ mkdir ~/bin
$ curl http://commondatastorage.googleapis.com/git-repo-downloads/repo  > ~/bin/repo
$ chmod a+x ~/bin/repo
$ PATH=${PATH}:~/bin
```
To execute
```
$: mkdir <release>
$: cd <release>
$: repo init -u https://github.com/edgehook/rk-linux-manifests.git -b <branch name> [ -m <release manifest>]
$: repo sync
```
Examples:To download the RK3399 itb201 release.
```
$repo init -u https://github.com/edgehook/rk-linux-manifests.git  -b rk3399_linux_v231_risc -m adv-rk3399-itb201a1-1.0.0.xml
$repo sync
```
## Build Method
### Build u-boot
```
$:<release># ./build.sh uboot
```
The generated file is located in the U-boot directory，include rk3399_loader_v1.24.119.bin、trust.img and uboot.img

### Build kernel

```
$:<release># ./build.sh kernel
```
The generated file is located in the kernel directory，is boot.img

### Build recovery

```
$:<release># rm -rf buildroot/output/rockchip_rk3399_recovery/
$:<release># source envsetup.sh rockchip_rk3399_recovery
$:<release># ./build.sh recovery
```
The generated file is located in the buildroot/output/rockchip_rk3399_recovery/images directory，is recovery.img

### Build Debian rootfs

Use the linaro-stretch-alip-whole-tar.gz file in the Debian directory to compile the file as follows
```
$:<release># rm -rf buildroot/output/rockchip_rk3399/
$:<release># source envsetup.sh rockchip_rk3399
$:<release># ./mk-debian.sh
```
Do not use the linaro-stretch-alip-whole-tar.gz file in the debian directory to compile the file as follows
```
$:<release># rm -rf buildroot/output/rockchip_rk3399/
$:<release># source envsetup.sh rockchip_rk3399
$:<release># ./mk-debian.sh new
```
Whichever way the above is compiled, the resulting file is located in the debian directory, is linaro-rootfs.img

### Build Ubuntu18.04 rootfs

Use the ubuntu18.04-whole.tar.gz file in the ubuntu directory to compile the file as follows
```
$:<release># rm -rf buildroot/output/rockchip_rk3399/
$:<release># source envsetup.sh rockchip_rk3399
$:<release># cd rootfs_adv/ubuntu18.04/
$:<release>/rootfs_adv/ubuntu18.04# ./mk-ubuntu.sh
```
Do not use the ubuntu18.04-whole.tar.gz file in the rootfs_adv/ubuntu18.04 directory to compile the file as follows
```
$:<release># rm -rf buildroot/output/rockchip_rk3399/
$:<release># source envsetup.sh rockchip_rk3399
$:<release># cd rootfs_adv/ubuntu18.04/
$:<release>/rootfs_adv/ubuntu18.04# ./mk-ubuntu.sh new
```
Whichever way the above is compiled, the resulting file is located in the ubuntu directory, is rootfs.img

## Push all image to rockdev folder

```
$:<release># ./mkfirmware.sh
```
All image in rockdev/ ./mkfirmware.sh at previous step will repack boot.img and rootfs.img, and copy other related image files to the rockdev/ directory. The common image files are listed below: 

```
board.img
boot.img -> ../kernel/boot.img
MiniLoaderAll.bin -> ../u-boot/rk3399_loader_v1.24.119.bin
misc.img -> ../device/rockchip/rockimg/wipe_all-misc.img
oem.img
parameter.txt -> ../device/rockchip/rk3399/parameter.txt
recovery.img -> ../buildroot/output/rockchip_rk3399_recovery/images/recovery.img
rootfs.img -> ../rootfs-adv/ubuntu18.04/rootfs.img
trust.img -> ../u-boot/trust.img
uboot.img -> ../u-boot/uboot.img
update.img
userdata.img
```
In mkfirmware.sh script, rootfs.img symbol link to debian/linaro-rootfs.img by default, and you can modify the symbol link to rootfs_adv/ubuntu18.04/rootfs.img by changing parameter RK_ROOTFS_IMG in device/rockchip/.BoardConfig.mk if necessary.

## Make update.img

```
$:<release># ./build.sh updateimg
```
The generated file is located in the rockdev directory.
