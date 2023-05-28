# Boot

## OS boot order
1. UEFI firmware
    - find some elf file at `/boot/efi/EFI/xxx/xxx.efi`
2. GRUB (bootloader)
3. Kernel (vmlinuz)
4. initramfs (initrd.img)
    - A small file system embedded in Linux kernel image
    - Helps the kernel to mount the root file system
5. PID 1 (systemd)

## Real Mode

## From Real Mode to Protected Mode
There are several things to do when changing from real mode to protected mode
1. 启用分段, 在内存里建立段描述符表, 将寄存器里面的 **段寄存器** 变为 **段选择子**, 指向某个段描述符, 这样就能实现不同进程的切换了
2. 启用分页
3. 打开Gate A20,  也就是第21根地址线的控制线

## Reference
[(1) David Hand _ "Linux initramfs for fun, and, uh..." - YouTube](https://www.youtube.com/watch?v=KQjRnuwb7is)
