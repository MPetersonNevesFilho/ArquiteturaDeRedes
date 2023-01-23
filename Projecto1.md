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
        no shutdown

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

            router rip
            version 2
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

### router 3
* nat/pat
        
        ip nat pool MYNATPOOL 195.5.5.80 195.5.5.85 netmask 255.255.255.240
        access-list 2 permit 10.10.0.0 0.0.0.16
        ip nat inside source list 2 pool MYNATPOOL overload
        interface f0/0
        ip nat inside
        interface f1/0
        ip nat inside
        interface f1/1
        ip nat outside


### router 2
* RIP

        conf t 
        router rip
        network 195.5.5.0
        no auto-summary 
        


### router 3
* IP configure

        conf t
        interface fe1/0
        ip address 191.1.1.253 255.255.255.252
        no shutdown

* RIP

        conf t 
        router rip
        network 195.5.5.0
        no auto-summary


* Rota Estática 
 
        ip route 195.5.5.128/27 191.1.1.254  
        

### router 4
* config ip

        conf t
        interface fe0/0
        ip address 191.1.1.254 255.255.255.252
        no shutdown
        

* rota estática

        ip route 195.5.5.92/28 191.1.1.253
        ip route 195.5.5.64/27 191.1.1.253
        ip route 195.5.5.0/27 191.1.1.253
        ip route 195.5.5.96/27 191.1.1.253
        ip route 195.5.5.160/28 191.1.1.253
        ip route 195.5.5.32/27 191.1.1.253
        ip route 100.100.100.0/24 191.1.1.253

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




