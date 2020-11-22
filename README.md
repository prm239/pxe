# pxe


 virt-install -n xyz -r 2048 --disk path=/var/lib/libvirt/images/xyz.qcow2,format=qcow2,size=20 -w network=pxe-net --pxe --graphics vnc,listen=0.0.0.0 

 virt-install -n xyz -r 2048 --disk path=/var/lib/libvirt/images/xyz.qcow2,format=qcow2,size=20 -w network=pxe-net --pxe --graphics vnc,listen=0.0.0.0 --boot uefi

virsh undefine xyz --nvram

yum install tftp-server
systemctl start tftp.socket 
systemctl start tftp.service

firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: ens3 ens6
  sources: 
  services: cockpit dhcp dhcpv6-client http proxy-dhcp ssh tftp
  ports: 
  protocols: 
  masquerade: no
  forward-ports: 
  source-ports: 
  icmp-blocks: 
  rich rules: 


rpm2cpio syslinux-tftpboot-6.04-4.el8.noarch.rpm | cpio -divm
mkdir /var/tftpboot/pxelinux.cgf
vi /var/tftpboot/pxelinux.cgf/default



rpm2cpio grub2-efi-x64-2.02-81.el8.x86_64.rpm | cpio -divm
rpm2cpio shim-x64-15-11.el8.x86_64.rpm | cpio -divm
cp efi/EFI/centos/shimx64.efi /var/lib/tftpboot/shim.efi
cp boot/efi/EFI/centos/grubx64.efi /var/lib/tftpboot/	
