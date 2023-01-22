### ESW1
* vlans

        vlan database
        vlan 1
        vlan 2
        vlan 3
        vlan 4
        exit
        config t

        ip routing


        ! Datacenter routing
        interface FastEthernet0/1
        ip address 195.5.5.161 255.255.255.240
        no shutdown

        interface Fastethernet 1/10
        ip address 195.5.5.79 255.255.255.240
        no shutdown

        interface range fastethernet 1/13 - 15
        switchport mode trunk
        switchport trunk encapsulation dot1q

        interface vlan 2
        ip address 195.5.5.98 255.255.255.224
        no autostate

        interface vlan 3 
        ip address 195.5.5.2 255.255.255.224
        no autostate

        interface vlan 4
        ip address 195.5.5.66 255.255.255.224
        no autostate

* OSPF 

        conf t
        
        router ospf 1

        network 195.5.5.160 0.0.0.15 area 0

        network 195.5.5.64 0.0.0.31 area 0

        network 195.5.5.0 0.0.0.31 area 0

        network 195.5.5.96 0.0.0.31 area 0

        network 195.5.5.32 0.0.0.31 area 0

        network 195.5.5.192 0.0.0.15 area 0

        network 195.5.5.128 0.0.0.31 area 0

        end
        write

### ESW2 
* vlan 

        vlan database
        vlan 1
        vlan 2
        vlan 3
        vlan 4
        exit
        config t
        ip routing

        ! data center routing
        interface FastEthernet0/1
        ip address 195.5.5.162 255.255.255.240
        no shutdown

        interface FastEthernet1/10
        ip address 195.5.5.80 255.255.255.240

        interface range fastethernet 1/13 - 15
        switchport mode trunk
        switchport trunk encapsulation dot1q

        interface vlan 2
        ip address 195.5.5.97 255.255.255.224
        no autostate

        interface vlan 3 
        ip address 195.5.5.1 255.255.255.224
        no autostate

        interface vlan 4
        ip address 195.5.5.65 255.255.255.224
        no autostate



* RIP OU Rota estática
    * RIP

            version 2
            router rip
            network 195.5.5.0
            no auto-summary
            end

    * Rota Estatica old building e Site b

            ip route 195.5.5.32/27 195.5.5.33  
            ip route 195.5.5.128/27 195.5.5.33


* OSPF 

        router ospf 1

        network 195.5.5.160 0.0.0.15 area 0

        network 195.5.5.64 0.0.0.31 area 0

        network 195.5.5.0 0.0.0.31 area 0

        network 195.5.5.96 0.0.0.31 area 0

        network 195.5.5.32 0.0.0.31 area 0
        
        network 195.5.5.128 0.0.0.31 area 0

        network 195.5.5.192 0.0.0.15 area 0

        end 
        write



### router 2



### router 3


### router 4



## Managment
### PC1
    ip 195.5.5.99 255.255.255.224 195.5.5.97

    
### PC2
    ip 195.5.5.100 255.255.255.224 195.5.5.97

## Engineering
### PC3
    ip 195.5.5.3 255.255.255.224 195.5.5.1

### PC4 
    ip 195.5.5.4 255.255.255.224 195.5.5.1

## VOIP

### PC5 
    ip 195.5.5.67 255.255.255.224 195.5.5.65

### PC6 
    ip 195.5.5.68 255.255.255.224 195.5.5.65




