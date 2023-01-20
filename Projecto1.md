### ESW1

    vlan database
    vlan 1
    vlan 2
    vlan 3
    exit
    config t

    ip routing

    interface FastEthernet0/1
    ip address 195.5.5.161 255.255.255.240
    no shutdown

    interface Fastethernet 1/10
    ip address 195.5.5.79 255.255.255.240
    no shutdown

    interface range fastethernet 1/13 - 15
    switchport mode trunk
    switchport trunk encapsulation dot1q

    interface vlan 1
    ip address 195.5.5.98 255.255.255.224
    no autostate

    interface vlan 2 
    ip address 195.5.5.2 255.255.255.224
    no autostate

    interface vlan 3
    ip address 195.5.5.66 255.255.255.224
    no autostate

    router ospf 1

    network 195.5.5.160 0.0.0.15 area 0

    network 195.5.5.64 0.0.0.31 area 0

    network 195.5.5.0 0.0.0.31 area 0

    network 195.5.5.96 0.0.0.31 area 0

    end
    write

### ESW2 

    vlan database
    vlan 1
    vlan 2
    vlan 3
    exit
    config t
    ip routing

    interface FastEthernet0/1
    ip address 195.5.5.162 255.255.255.240
    no shutdown

    interface FastEthernet1/10
    ip address 195.5.5.80 255.255.255.240

    interface range fastethernet 1/13 - 15
    switchport mode trunk
    switchport trunk encapsulation dot1q

    interface vlan 1
    ip address 195.5.5.97 255.255.255.224
    no autostate

    interface vlan 2 
    ip address 195.5.5.1 255.255.255.224
    no autostate

    interface vlan 3
    ip address 195.5.5.65 255.255.255.224
    no autostate

    
    router ospf 1

    network 195.5.5.160 0.0.0.15 area 0

    network 195.5.5.64 0.0.0.31 area 0

    network 195.5.5.0 0.0.0.31 area 0

    network 195.5.5.96 0.0.0.31 area 0

    end 
    write


