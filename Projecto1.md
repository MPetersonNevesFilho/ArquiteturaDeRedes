## L3SWA
* vlans

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
		
* Database

		conf t
		interface f0/0
		no switchport ! to no make it part of any vlan
		ip address 195.5.5.161 255.255.255.240
		no shutdown
		exit
		
		end
		write


* connection to router 1

		conf t
		interface f1/0
		no switchport
		ip address 10.10.0.5 255.255.255.252
		no shutdown 
		exit
		
		end
		write

## L3SWB

* vlans

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
		no autostate
		interface Vlan 3
		ip address 195.5.5.1 255.255.255.224
		no autostate
		interface Vlan 4
		ip address 10.10.2.1 255.255.255.0 
		no autostate 
		exit 
		
		end 
		write

	
* Database

		conf t
		interface f0/0
		no switchport
		ip address 195.5.5.162 255.255.255.240
		no shutdown
		exit
		
		end
		write
		

* connection to router 1

		conf t
		interface f1/0
		no switchport
		ip address 10.10.0.2 255.255.255.252
		no shutdown 
		exit
		
		end
		write
		
		
## Router 1
		
		conf t
		interface f1/0
		ip address 10.10.0.6 255.255.255.252
		no shutdown
		exit
		
		interface f1/1
		ip address 10.10.0.1 255.255.255.252
		no shutdown
		exit
		
		end
		write

## PCS

### Managment
* PC 1

		ip 10.10.1.5 255.255.255.0 10.10.1.1


### Engineering
* PC1 

		ip 195.5.5.5 255.255.255.224 195.5.5.1


### VOIP
* PC1

		ip 10.10.2.5 255.255.255.0 10.10.2.1
		
### Database
* PC1

		ip 195.5.5.165 255.255.255.240 195.5.5.161

