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
	
