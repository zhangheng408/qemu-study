1.create img
    qemu-img create -f qcow2 ubuntu.img 10G
2.boot iso
    mount ubuntu-16.04.3-server-amd64.iso /mnt
    qemu-system-x86_64 -m 1024 -hda ubuntu.img -cdrom ubuntu-16.04.3-server-amd64.iso --nographic -append console=ttyS0 -kernel /mnt/install/vmlinuz -initrd /mnt/install/initrd.gz 
