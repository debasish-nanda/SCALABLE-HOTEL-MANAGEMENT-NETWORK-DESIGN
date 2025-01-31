SCALABLE HOTEL MANAGEMENT NETWORK DESIGN:

In this project, a network infrastructure has been designed and implemented for a hotel with various departments. The hotel network consists of multiple VLANs for different departments, ensuring efficient 
communication, security, and resource management across the organization. The VLANs are organized to ensure that each department has a dedicated network, and a guest VLAN is isolated from the rest to protect 
internal data and resources.

Network Design and Architecture: 
The network is structured into 5 VLANs:
-	VLAN 10: Reception
-	VLAN 20: Finance
-	VLAN 30: Restaurant
-	VLAN 40: Sales
-	VLAN 50: Guest (isolated for guest PCs) 

Each of these VLANs is associated with a specific department in the hotel. The guest VLAN is isolated from all the other VLANs using Access Control Lists (ACLs), which prevent guest PCs from communicating 
with internal networks. However, internal networks (Reception, Finance, Restaurant, and Sales) can communicate with each other as needed. 

The core components of the design include:
  - Switches: Used to manage the VLAN segmentation for different departments.
  - Router: Handles the inter-VLAN routing, ensuring communication between VLANs.
 - Access Control Lists (ACLs): Used to control the traffic flow between the VLANs and ensure
    security


IP Addressing Scheme: 
The network uses the following IP addressing scheme to ensure proper communication and segmentation of the departments:
VLAN	Department	 IP Range	Subnet Mask	Gateway
10	Reception	192.168.10.0 - 192.168.10.3	255.255.255.0	192.168.10.1
20	Finance	192.168.20.0 - 192.168.20.3	255.255.255.0	192.168.20.1
30	Restaurant	192.168.30.0 - 192.168.30.3	255.255.255.0	192.168.30.1
40	Sales	192.168.40.0 - 192.168.40.3	255.255.255.0	192.168.40.1
50	Guest	192.168.50.0 - 192.168.50.3	255.255.255.0	192.168.50.1
 
   






Each department has a dedicated VLAN with 3 PCs in each subnet. The IP addresses of these PCs are statically assigned as follows:
- Reception VLAN (VLAN 10):
  - PC1: 192.168.10.2
 - PC2: 192.168.10.3
 - PC3: 192.168.10.4 
- Finance VLAN (VLAN 20):
 - PC1: 192.168.20.2 
- PC2: 192.168.20.3 
- PC3: 192.168.20.4
- Restaurant VLAN (VLAN 30): 
- PC1: 192.168.30.2
 - PC2: 192.168.30.3 
- PC3: 192.168.30.4
- Sales VLAN (VLAN 40):
 - PC1: 192.168.40.2
 - PC2: 192.168.40.3
 - PC3: 192.168.40.4
- Guest VLAN (VLAN 50):
 - PC1: 192.168.50.2
 - PC2: 192.168.50.3
 - PC3: 192.168.50.4 

Switch Configuration: 
The switches are configured with the following VLAN settings: 
 vlan 10 
 name reception 
 vlan 20 
 name finance 
 vlan 30 
 name restaurant 
 vlan 40 
 name sales 
 vlan 50 
 name guest
 
Here, the VLANs are created on the switches and are associated with specific departments in the hotel. The naming convention used for the VLANs ensures that they are easily identifiable based on the department 
they correspond to.

 Port Assignments: 
The network interfaces (FastEthernet ports) are assigned to the respective VLANs. Each VLAN will use 3 ports to connect the PCs in the respective departments:
 interface range fastethernet 0/2 - 0/4
 switchport mode access switchport access vlan 10 // Reception VLAN 
 interface range fastethernet 0/5 - 0/7 
 switchport mode access switchport access vlan 20 // Finance VLAN 
 interface range fastethernet 0/8 - 0/10 
 switchport mode access 
 switchport access vlan 30 // Restaurant VLAN 
 interface range fastethernet 0/11 - 0/13 
 switchport mode access 
 switchport access vlan 40 // Sales VLAN 
 interface range fastethernet 0/14 - 0/16 
 switchport mode access 
 switchport access vlan 50 // Guest VLAN 

Router Configuration: 
The router acts as the gateway between the VLANs, providing inter-VLAN communication. The router is configured to handle traffic between VLANs as follows: 
 interface gig0/0.10 
 encapsulation dot1Q 10 
 ip address 192.168.10.1 255.255.255.0 
 interface gig0/0.20 
 encapsulation dot1Q 20 
 ip address 192.168.20.1 255.255.255.0 
 interface gig0/0.30 
 encapsulation dot1Q 30 
 ip address 192.168.30.1 255.255.255.0 
 interface gig0/0.40 
 encapsulation dot1Q 40 
 ip address 192.168.40.1 255.255.255.0 
 interface gig0/0.50 
 encapsulation dot1Q 50 
 ip address 192.168.50.1 255.255.255.0 
 ip access-group 101 in

 Each sub-interface corresponds to a specific VLAN, and the router is configured with IP addresses as the default gateways for each VLAN. The router also handles inter-VLAN routing to ensure that devices 
 in different VLANs can communicate with each other. 

Access Control Lists (ACLs): 
Access Control Lists (ACLs) are implemented to restrict communication between the VLANs. Specifically, the guest VLAN (VLAN 50) is isolated from the rest of the VLANs, preventing guest PCs from accessing 
internal resources. The ACL configuration is as follows: 
 access-list 101 deny ip 192.168.10.0 0.0.0.255 192.168.50.0 0.0.0.255 
 access-list 101 deny ip 192.168.20.0 0.0.0.255 192.168.50.0 0.0.0.255 
 access-list 101 deny ip 192.168.30.0 0.0.0.255 192.168.50.0 0.0.0.255 
 access-list 101 deny ip 192.168.40.0 0.0.0.255 192.168.50.0 0.0.0.255 
 access-list 101 permit ip any any 

This ACL denies all communication from the internal VLANs (10, 20, 30, 40) to the guest VLAN (50) while allowing all other traffic. This ensures that the guest VLAN is isolated for security purposes. 

This network design ensures that each department in the hotel has its own isolated network, improving performance, security, and management. The guest network is also isolated using ACLs, ensuring that 
guests cannot access internal resources. The network is efficient, secure, and scalable for future growth 
