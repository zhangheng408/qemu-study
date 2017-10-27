require:
    sudo apt install qemu-kvm libvirt-bin virt-manager bridge-utils qemu

1.create img
    qemu-img create -f qcow2 ubuntu.img 10G
2.boot iso
    mount ubuntu-16.04.3-server-amd64.iso /mnt
    qemu-system-x86_64 -m 1024 -hda ubuntu.img -cdrom ubuntu-16.04.3-server-amd64.iso --nographic -append console=ttyS0 -kernel /mnt/install/vmlinuz -initrd /mnt/install/initrd.gz 

3.edit qcow2 img
    //mount
    modprobe nbd max_part=8
    qemu-nbd -c /dev/nbd0 test.qcow2
    mount /dev/nbd0p1 /mnt/img/

    //umount
    umount /mnt/img
    qemu-nbd -d /dev/ndb0

4.run ubuntu img
    qemu-system-x86_64 -m 3000 -hda ubuntu.img -nographic -net user,hostfwd=tcp::99522-:22 -net nic
