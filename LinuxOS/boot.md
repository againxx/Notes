# Boot

## OS boot order
1. UEFI firmware
    - find some elf file at `/boot/efi/EFI/xxx/xxx.efi`
2. GRUB (bootloader)
3. Kernel (vmlinuz)
4. initramfs (initrd.img)
    - A small filesystem embedded in Linux kernel image
    - Helps the kernel to mount the root filesystem
5. PID 1 (systemd)

## Reference
[(1) David Hand _ "Linux initramfs for fun, and, uh..." - YouTube](https://www.youtube.com/watch?v=KQjRnuwb7is)
