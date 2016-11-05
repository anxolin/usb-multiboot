# USB Multi-boot
Grub2 multiboot USB instalation and configuration based on glim and with vimix theme.

## USB creation
>Based on [[https://wiki.archlinux.org/index.php/Multiboot_USB_drive]]

Assuming the USB is on `sdc`:
  * **/dev/sdc1** (1M): BIOS type. Where grub installs the MBR for BIOS compatibility.
  * **/dev/sdc2** (512M): FAT32 type. UEFI System Partition. Where the grub's EFI application is installed.
  * **/dev/sdc3** (Remaining space): ReiserFS type. Data and grub instalation with all the ditribtion's ISOs.


Grub UEFI:
```bash
grub-install --target=x86_64-efi --efi-directory=/mnt/usb --boot-directory=/mnt/aux --removable --recheck
```

Grub BIOS:
```bash
grub-install --target=i386-pc --boot-directory=/mnt/aux/boot --recheck /dev/sdc
```

## Folders in **/dev/sdc3**
  * `boot/iso`: Folder with the disto's ISOs
  * `boot/grub`: Grub instalation for BIOS and UEFI
  * `grub`: Grub instalation for UEFI (it's just a simbolic link to boot/grub)

## Backup
```bash
sudo tar --exclude './backup' --exclude './boot/iso' -zcvf './backup/grub.2016.11.05-2.tar.gz' .
```
