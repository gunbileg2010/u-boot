# Samsung Galaxy A14 4G (SM-A145F) — U-Boot chainload

Runs as the "kernel" in boot.img; the stock S-Boot hands over its FDT and the
board code (exynos-mobile) takes DRAM banks and the framebuffer from it.

    make a145f_defconfig
    make CROSS_COMPILE=aarch64-linux-gnu- -j$(nproc)
    python3 board/samsung/exynos-mobile/a145f/pack_boot_v4.py u-boot.bin \
        --stock <your stock boot.img> -o boot_uboot.img
    heimdall flash --BOOT boot_uboot.img

Recovery: boot download mode (Vol Down + Vol Up while plugging USB) and flash
the stock boot.img again. Device tree: dts/upstream/src/arm64/exynos/exynos850-a145f.dts
(derived from the A135F one; memory map, SD (dwmmc2) and keys from the live A145F DTB).
Untested on hardware: SD card clock/timing values, USB gadget (VBUS is left to S-Boot).
