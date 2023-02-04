## L3SWA
* vlans

		conf t
		ipv6 unicast-routing
		ipv6 router ospf 1
		exit
		exit


		vlan database
		vlan 1
		vlan 2
		vlan 3
		vlan 4
		exit
		
		conf t
		ip routing 
		interface f1/0
		switchport mode access
		switchport access vlan 1
		interface range fastEthernet 1/5 - 7
		switchport mode access
		switchport access vlan 2
		interface range fastEthernet 1/8 - 10 
		switchport mode access               
		switchport access vlan 3             
		interface range fastEthernet 1/11 - 13
		switchport mode access                
		switchport access vlan 4              
		interface range fastEthernet 1/13 - 15
		switchport mode trunk
		switchport trunk encapsulation dot1q
		exit
		
		interface vlan 2
		ip address 10.10.1.2 255.255.255.0
		ipv6 address 2200:0:0:2::2/64
		ipv6 ospf 1 area 0
		no autostate
		interface Vlan 3
		ip address 195.5.5.2 255.255.255.224
		ipv6 address 2200:0:0:3::2/64
		ipv6 ospf 1 area 0
		no autostate
		interface Vlan 4
		ip address 10.10.2.2 255.255.255.0 
		ipv6 address 2200:0:0:4::2/64
		ipv6 ospf 1 area 0
		no autostate 
		exit 
	
		end 
		write
		
* Database

		conf t
		interface f0/0
		ipv6 enable
		no switchport ! to no make it part of any vlan
		ip address 195.5.5.161 255.255.255.240
		ipv6 address 2200:0:0:1::2/64
		ipv6 ospf 1 area 0
		ip ospf 1 area 0
		no shutdown
		exit
		
		end
		write


* connection to router 1

		conf t
		interface f1/0
		ipv6 enable
		no switchport
		ip address 10.10.0.5 255.255.255.252
		ipv6 address 2200:0:0:10::2/64
		ipv6 ospf 1 area 0
		ip ospf 1 area 0
		no shutdown 
		exit

		router ospf 1
		network 10.10.1.0 255.255.255.0 area 0
		network 10.10.2.0 255.255.255.0 area 0
		network 195.5.5.0 255.255.255.224 area 0
		exit

		
		end
		write


## L3SWB

* vlans

		conf t
		ipv6 unicast-routing
		ipv6 router ospf 1
		exit
		exit

		vlan database
		vlan 1
		vlan 2
		vlan 3
		vlan 4
		exit
		
		conf t
		ip routing 
		interface f1/0
		switchport mode access
		switchport access vlan 1
		interface range fastEthernet 1/5 - 7
		switchport mode access
		switchport access vlan 2
		interface range fastEthernet 1/8 - 10 
		switchport mode access               
		switchport access vlan 3             
		interface range fastEthernet 1/11 - 13
		switchport mode access                
		switchport access vlan 4              
		interface range fastEthernet 1/13 - 15
		switchport mode trunk
		switchport trunk encapsulation dot1q
		exit
		
		interface vlan 2
		ip address 10.10.1.1 255.255.255.0
		ipv6 address 2200:0:0:2::1/64
		ipv6 ospf 1 area 0
		no autostate
		interface Vlan 3
		ip address 195.5.5.1 255.255.255.224
		ipv6 address 2200:0:0:3::1/64
		ipv6 ospf 1 area 0
		no autostate
		interface Vlan 4
		ip address 10.10.2.1 255.255.255.0
		ipv6 address 2200:0:0:4::1/64 
		ipv6 ospf 1 area 0
		no autostate 
		exit 
		
		end 
		write

	
* Database

		conf t
		interface f0/0
		ipv6 enable
		no switchport
		ip address 195.5.5.162 255.255.255.240
		ipv6 address 2200:0:0:1::1/64
		ipv6 ospf 1 area 0
		ip ospf 1 area 0
		no shutdown
		exit
		
		end
		write
		

* connection to router 1

		conf t
		interface f1/0
		ipv6 enable
		no switchport
		ip address 10.10.0.2 255.255.255.252
		ipv6 address 2200:0:0:9::2/64
		ipv6 ospf 1 area 0
		ip ospf 1 area 0
		no shutdown 
		exit


		router ospf 1
		network 10.10.1.0 255.255.255.0 area 0
		network 10.10.2.0 255.255.255.0 area 0
		network 195.5.5.0 255.255.255.224 area 0
		exit
		
		end
		write

* connection to router 2


		conf t 
		router rip
		version 2
		network 10.10.1.0
		network 195.5.5.0 
		network 10.10.2.0
		network 195.5.5.160
		network 10.10.0.8
		network 195.5.5.192
		exit
		
		interface f0/1
		ipv6 enable
		no switchport
		ip address 10.10.0.9 255.255.255.252
		ipv6 address 2200:0:0:7::1/64
		ipv6 ospf 1 area 0
		ip ospf 1 area 0
		ipv6 rip 1 enable
		no shutdown
		exit

		end
		write

* redestribute ripng and ospfv3

		


		conf t
		ipv6 router ospf 1
		redistribute rip RIPNG
		exit
		
		router rip
		redistribute connected 
		redistribute ospf 1 metric 1
		exit
		
		router ospf 1
		redistribute rip
		redistribute connected 
		exit

		ipv6 router rip RIPNG
		redistribute connected 
		redistribute ospf 1 metric 1
		exit
		
		end 
		write

		
		
## Router 1
		
		conf t
		ipv6 unicast-routing
		ipv6 router ospf 1
		exit
		
		interface f1/0
		ipv6 enable
		ip address 10.10.0.6 255.255.255.252
		ipv6 address 2200:0:0:10::1/64
		ipv6 ospf 1 area 0
		ip ospf 1 area 0
		no shutdown
		exit
		
		interface f1/1
		ipv6 enable
		ip address 10.10.0.1 255.255.255.252
		ipv6 address 2200:0:0:9::1/64
		ipv6 ospf 1 area 0
		ip ospf 1 area 0
		no shutdown
		exit
		
		interface f2/0
		ipv6 enable
		ip address 195.5.5.193 255.255.255.240
		ipv6 address 2200:0:0:0::1/64
		ipv6 ospf 1 area 0
		ip ospf 1 area 0
		no shutdown
		exit
		
		end
		write


## Router 2


		conf t
		ipv6 unicast-routing
		ipv6 router ospf 1
		exit


		router rip
		version 2
		network 195.5.5.32
		network 10.10.0.8
		exit
		
		interface f1/0
		ipv6 enable
		ip address 10.10.0.10 255.255.255.252
		ipv6 address 2200:0:0:7::2/64
		ipv6 rip 1 enable
		ipv6 ospf 1 area 0
		no shutdown
		exit

		interface f0/0
		ipv6 enable
		ip address 195.5.5.33 255.255.255.224
		ipv6 address 2200:0:0:5::1/64
		ipv6 rip 1 enable
		no shutdown
		exit

		end
		write

* redestribute ripng and ospfv3


		conf t
		ipv6 router ospf 1
		redistribute rip RIPNG
		exit
		ipv6 router rip RIPNG
		redistribute connected 
		redistribute ospf 1 metric 1
		exit
		end 
		write

## Router 3

		conf t
		ipv6 unicast-routing
		ipv6 router ospf 1
		exit

		router rip
		version 2
		network 195.5.5.32
		network 191.1.1.252
		network 195.5.5.128
		exit

		interface f0/0	
		ipv6 enable
		ip address 195.5.5.34 255.255.255.224
		ipv6 address 2200:0:0:5::1/64
		ipv6 rip 1 enable
		no shutdown
		exit

		interface f1/0	
		ipv6 enable
		ip address 191.1.1.253 255.255.255.252
		ipv6 address 2200:0:0:8::1/64
		no shutdown
		exit

		ip route 195.5.5.128 255.255.255.224 191.1.1.254


		router rip
		redistribute connected
		redistribute static
		exit
		
		ipv6 router rip RIPNG
		redistribute connected
		redistribute static
		exit

		end
		write


## router 4

		conf t
		
		interface f0/0
		ipv6 enable
		ip address 191.1.1.254 255.255.255.252
		ipv6 address 2200:0:0:8::2/64
		no shutdown
		exit

		interface f1/0
		ipv6 enable
		ip address 195.5.5.129 255.255.255.224
		ipv6 address 2200:0:0:6::1/64
		no shutdown
		exit 	

		ip route 195.5.5.0 255.255.255.224 191.1.1.253
		ip route 195.5.5.192 255.255.255.240 191.1.1.253
		ip route 195.5.5.160 255.255.255.240 191.1.1.253
		ip route 195.5.5.76 255.255.255.240 191.1.1.253
		ip route 10.10.0.0 255.255.0.0 191.1.1.253
		ip route 100.100.100.0 255.255.255.0 191.1.1.253

		end 
		write	



## PCS

### Managment
* PC 1

		ip 10.10.1.5 255.255.255.0 10.10.1.1
		ip 2200:0:0:2::5/64

### Engineering
* PC1 

		ip 195.5.5.5 255.255.255.224 195.5.5.1
		ip 2200:0:0:3::5/64


### VOIP
* PC1

		ip 10.10.2.5 255.255.255.0 10.10.2.1
		ip 2200:0:0:4::5/64
		
### Database
* PC1

		ip 195.5.5.165 255.255.255.240 195.5.5.161
		ip 2200:0:0:1::5/64
		
### DMZ

* PC1
		ip 195.5.5.195 255.255.255.240 195.5.5.193
		ip 2200:0:0:0::5/64


