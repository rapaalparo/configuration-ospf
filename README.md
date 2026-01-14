========================================
OSPF CONFIGURATION
CISCO PACKET TRACER
========================================

TOPOLOGY
PC1 ---- R1 ---- R2 ---- PC2

========================================
IP ADDRESSING
========================================
PC1 : 192.168.1.10/24   GW 192.168.1.1
PC2 : 192.168.2.10/24   GW 192.168.2.1

R1 G0/0 : 192.168.1.1/24
R1 G0/1 : 10.10.10.1/30

R2 G0/0 : 10.10.10.2/30
R2 G0/1 : 192.168.2.1/24

========================================
ROUTER 1 CONFIGURATION (OSPF AREA 0)
========================================
enable
configure terminal
hostname R1

interface g0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
exit

interface g0/1
 ip address 10.10.10.1 255.255.255.252
 no shutdown
exit

router ospf 1
 router-id 1.1.1.1
 network 192.168.1.0 0.0.0.255 area 0
 network 10.10.10.0 0.0.0.3 area 0
exit

end
write memory

========================================
ROUTER 2 CONFIGURATION (OSPF AREA 0)
========================================
enable
configure terminal
hostname R2

interface g0/0
 ip address 10.10.10.2 255.255.255.252
 no shutdown
exit

interface g0/1
 ip address 192.168.2.1 255.255.255.0
 no shutdown
exit

router ospf 1
 router-id 2.2.2.2
 network 10.10.10.0 0.0.0.3 area 0
 network 192.168.2.0 0.0.0.255 area 0
exit

end
write memory

========================================
VERIFICATION
========================================
R1# show ip ospf neighbor
R1# show ip route ospf

R2# show ip ospf neighbor
R2# show ip route ospf

========================================
TESTING
========================================
PC1> ping 192.168.2.10
