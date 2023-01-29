### ESW1
* vlans

	vlan database
	vlan 1
	vlan 2
	vlan 3
	vlan 4
	
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
	no autostate
	interface Vlan 3
	ip address 195.5.5.2 255.255.255.224
	no autostate
	interface Vlan 4
	ip address 10.10.2.2 255.255.255.0 
	no autostate 
	exit 
	
	end 
	write

	
	
	
