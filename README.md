# ccna-ospf-

	You are currently connected to R2:
• Enter the OSPF router configuration mode using process ID 10
• Configure R2’s router ID as 2.2.2.2
R2(config)#router ospf 10
R2(config-router)#router-id 2.2.2.2
R2(config-router)#
	Advertise the networks connected to R2 with the appropriate wildcard mask in Area 0. Configure the networks in the following order:
1.	10.10.2.0/24
2.	10.1.1.4/30
3.	10.1.1.8/30
R2(config-router)#network 10.10.2.0 0.0.0.255 area 0
R2(config-router)#network 10.1.1.4 0.0.0.3 area 0
R2(config-router)#network 10.1.1.8 0.0.0.3 area 0
R2(config-router)#
*Mar 25 21:19:21.938: %OSPF-5-ADJCHG: Process 10, Nbr 1.1.1.1 on GigabitEthernet0/0/0 from LOADING to FULL, Loading Done
	You are now configuring R3:
• Enter OSPF router configuration mode using process ID 10
• Configure R3’s router ID
• Use the network statement to enable OSPF based on the interface address with a quad-zero wildcard mask for Area 0
• Return to privileged EXEC mode when finished.
R3(config)#router ospf 10
R3(config-router)#router-id 3.3.3.3
R3(config-router)#
	Use the network statement to enable OSPF based on the interface address with a quad-zero wildcard mask for Area 0. Configure the interfaces in the following order:
1.	10.10.3.1
2.	10.1.1.10
3.	10.1.1.13
R3(config-router)#network 10.10.3.1 0.0.0.0 area 0
R3(config-router)#network 10.1.1.10 0.0.0.0 area 0
R3(config-router)#network 10.1.1.13 0.0.0.0 area 0
R3(config-router)#
*Mar 26 14:00:55.183: %OSPF-5-ADJCHG: Process 10, Nbr 1.1.1.1 on GigabitEthernet0/0/0 from LOADING to FULL, Loading Done
*Mar 26 14:00:55.243: %OSPF-5-ADJCHG: Process 10, Nbr 2.2.2.2 on GigabitEthernet0/0/1 from LOADING to FULL, Loading Done
R3#
You have successfully advertised the OSPF networks on R2 and R3.
	You are currently connected to R2. The network commands have already been removed. Configure OSPF routing using process ID 10, in Area 0, on each interface in the following order. Use the following abbreviated interface names:
•	lo0
•	g0/0/0
•	g0/0/1
R2(config)#interface lo0 
R2(config-if)#ip ospf 10 area 0 
R2(config-if)#interface g0/0/0 
R2(config-if)#ip ospf 10 area 0 
R2(config-if)#interface g0/0/1 
R2(config-if)#ip ospf 10 area 0 
*Mar 25 21:19:21.938: %OSPF-5-ADJCHG: Process 10, Nbr 1.1.1.1 on GigabitEthernet0/0/0 from LOADING to FULL, Loading Done
•	You are now connected to R3. The network commands have already been removed. Configure OSPF routing using process ID 10, in Area 0, on each interface in the following order. Use the following abbreviated interface names:
•	lo0
•	g0/0/0
•	g0/0/1
R3(config)#interface lo0
R2(config-if)#ip ospf 10 area 0
R2(config-if)#interface g0/0/0
R2(config-if)#ip ospf 10 area 0
R2(config-if)#interface g0/0/1
R2(config-if)#ip ospf 10 area 0
*Mar 26 14:00:55.183: %OSPF-5-ADJCHG: Process 10, Nbr 1.1.1.1 on GigabitEthernet0/0/0 from LOADING to FULL, Loading Done
*Mar 26 14:00:55.243: %OSPF-5-ADJCHG: Process 10, Nbr 2.2.2.2 on GigabitEthernet0/0/1 from LOADING to FULL, Loading Done
R3(config-router)#
You have successfully configured the interfaces to advertise the OSPF networks.
	You are currently connected to R2:
• Enter OSPF router configuration mode using process ID 10
• Configure the Loopback interface as passive using the abbreviated interface name lo0
• Return to privileged EXEC mode
*Verify the OSPF settings with the show ip protocols command.

R2(config)#router ospf 10
R2(config-router)#passive-interface lo0
R2(config-router)#end
*May 23 20:27:20.718: %SYS-5-CONFIG_I: Configured from console by console
R2#show ip protocols
***IP Routing is NSF aware***
(output omitted)
Routing Protocol is "ospf 10"
  Outgoing update filter list for all interfaces is not set
  Incoming update filter list for all interfaces is not set
  Router ID 2.2.2.2
  Number of areas in this router is 1. 1 normal 0 stub 0 nssa
  Maximum path: 4
  Routing for Networks:
  Routing on Interfaces Configured Explicitly (Area 0):
    Loopback0
    GigabitEthernet0/0/1
    GigabitEthernet0/0/0
  Passive Interface(s):
    Loopback0
  Routing Information Sources:
    Gateway         Distance      Last Update
    3.3.3.3              110      02:07:48
    1.1.1.1              110      02:34:53
  Distance: (default is 110)
R2#
	You are now logged into R3:
•	Enter OSPF router configuration mode using process ID 10
•	Use one command to configure all interfaces as passive
•	Use the shortened interface names g0/0/0 and g0/0/1 to remove these interfaces from the passive list
•	Return to privileged EXEC mode
•	Verify the OSPF settings with the show ip protocols command.
R3(config)#router ospf 10
R3(config-router)#passive-interface default
*Jun  5 23:06:46.668: %OSPF-5-ADJCHG: Process 10, Nbr 1.1.1.1 on GigabitEthernet0/0/0 from FULL to DOWN, Neighbor Down: Interface down or detached
*Jun  5 23:06:46.669: %OSPF-5-ADJCHG: Process 10, Nbr 2.2.2.2 on GigabitEthernet0/0/1 from FULL to DOWN, Neighbor Down: Interface down or detached
R3(config-router)#no passive-interface g0/0/0
*Jun  5 23:07:07.746: %OSPF-5-ADJCHG: Process 10, Nbr 1.1.1.1 on GigabitEthernet0/0/0 from LOADING to FULL, Loading Done
R3(config-router)#no passive-interface g0/0/1
*Jun  5 23:07:17.841: %OSPF-5-ADJCHG: Process 10, Nbr 2.2.2.2 on GigabitEthernet0/0/1 from LOADING to FULL, Loading Done
R3(config-router)#end
* Jun  5 23:07:35.732: %SYS-5-CONFIG_I: Configured from console by console
R3#show ip protocols
***IP Routing is NSF aware***
(output omitted)
Routing Protocol is "ospf 10"
  Outgoing update filter list for all interfaces is not set
  Incoming update filter list for all interfaces is not set
  Router ID 3.3.3.3
  Number of areas in this router is 1. 1 normal 0 stub 0 nssa
  Maximum path: 4
  Routing for Networks:
  Routing on Interfaces Configured Explicitly (Area 0):
    Loopback0
    GigabitEthernet0/0/1
    GigabitEthernet0/0/0
  Passive Interface(s):
    Serial0/1/0
    Serial0/1/1
    Loopback0
  Routing Information Sources:
    Gateway         Distance      Last Update
    1.1.1.1              110      00:00:59
    2.2.2.2              110      00:00:48
  Distance: (default is 110)
R3#
You have successfully configured passive interfaces on R2 and R3.
✓ Use the ip ospf priority command to modify the DR and BDR as follows:
• R1 should be the BDR and will be configured with a priority of 10
• R2 should never be a DR or BDR and will be configured with a priority of 0
• R3 should be the DR and will remain with the default priority of 100
On all routers, use g0/0/0 as the interface name.
You are connected to R1 in global configuration mode. Configure R1 with a priority of 10.
R1(config)#interface g0/0/0
R1(config-if)#ip ospf priority 10
R1(config-if)#
You are now connected to R2 in global configuration mode. Configure R2 with a priority of 0.

R2(config)#interface g0/0/0
R2(config-if)#ip ospf priority 0
R2(config-if)#
You are now connected to R3 in global configuration mode. Configure R3 with a priority of 100.
R3(config)#interface g0/0/0
R3(config-if)#ip ospf priority 100
R3(config-if)#
You are still connected to R3 in interface configuration mode. Return to privileged EXEC mode. Since R3 should be the DR, you need to restart the OSPF process on it first.
R3(config-if)#end
R3#clear ip ospf process
Reset ALL OSPF processes? [no]:y 
*Jun  5 05:29:35.231: %OSPF-5-ADJCHG: Process 10, Nbr 1.1.1.1 on GigabitEthernet0/0/0 from FULL to DOWN, Neighbor Down: Interface down or detached
*Jun  5 05:29:35.231: %OSPF-5-ADJCHG: Process 10, Nbr 2.2.2.2 on GigabitEthernet0/0/0 from FULL to DOWN, Neighbor Down: Interface down or detached
*Jun  5 05:29:35.235: %OSPF-5-ADJCHG: Process 10, Nbr 1.1.1.1 on GigabitEthernet0/0/0 from LOADING to FULL, Loading Done
*Jun  5 05:29:44.563: %OSPF-5-ADJCHG: Process 10, Nbr 2.2.2.2 on GigabitEthernet0/0/0 from LOADING to FULL, Loading Done
R3#
You are now connected to R1 in privileged EXEC mode. Since R1 is the DR, you need to restart the OSPF process next.

R1#clear ip ospf process
Reset ALL OSPF processes? [no]:y
*Jun  5 05:27:20.691: %OSPF-5-ADJCHG: Process 10, Nbr 2.2.2.2 on GigabitEthernet0/0/0 from FULL to DOWN, Neighbor Down: Interface down or detached
*Jun  5 05:27:20.691: %OSPF-5-ADJCHG: Process 10, Nbr 3.3.3.3 on GigabitEthernet0/0/0 from FULL to DOWN, Neighbor Down: Interface down or detached
*Jun  5 05:27:21.695: %OSPF-5-ADJCHG: Process 10, Nbr 2.2.2.2 on GigabitEthernet0/0/0 from LOADING to FULL, Loading Done
*Jun  5 05:27:20.951: %OSPF-5-ADJCHG: Process 10, Nbr 3.3.3.3 on GigabitEthernet0/0/0 from LOADING to FULL, Loading Done
R1#
You are now connected to R2 in privileged EXEC mode. R2 should be a DROTHER. Restart the OSPF process.

R2#clear ip ospf process
Reset ALL OSPF processes? [no]:y
*Jun  5 15:37:08.978: %OSPF-5-ADJCHG: Process 10, Nbr 1.1.1.1 on GigabitEthernet0/0/0 from 2WAY to DOWN, Neighbor Down: Interface down or detached
*Jun  5 15:37:08.978: %OSPF-5-ADJCHG: Process 10, Nbr 3.3.3.3 on GigabitEthernet0/0/0 from FULL to DOWN, Neighbor Down: Interface down or detached
*Jun  5 15:37:08.983: %OSPF-5-ADJCHG: Process 10, Nbr 1.1.1.1 on GigabitEthernet0/0/0 from LOADING to FULL, Loading Done
*Jun  5 15:37:19.477: %OSPF-5-ADJCHG: Process 10, Nbr 3.3.3.3 on GigabitEthernet0/0/0 from LOADING to FULL, Loading Done
R2#
You are now connected to R1. Use the show ip ospf interface g0/0/0 command to verify that R1 is the BDR.

R1#show ip ospf interface g0/0/0
GigabitEthernet0/0/0 is up, line protocol is up 
  Internet Address 192.168.1.1/24, Area 0, Attached via Interface Enable
  Process ID 10, Router ID 1.1.1.1, Network Type BROADCAST, Cost: 1
  Topology-MTID    Cost    Disabled    Shutdown      Topology Name
        0           1         no          no            Base
  Enabled by interface config, including secondary ip addresses
  Transmit Delay is 1 sec, State BDR, Priority 10
  Designated Router (ID) 3.3.3.3, Interface address 192.168.1.3
  Backup Designated router (ID) 1.1.1.1, Interface address 192.168.1.1
  Timer intervals configured, Hello 10, Dead 40, Wait 40, Retransmit 5
    oob-resync timeout 40
    Hello due in 00:00:04
  Supports Link-local Signaling (LLS)
  Cisco NSF helper support enabled
  IETF NSF helper support enabled
  Index 1/1/1, flood queue length 0
  Next 0x0(0)/0x0(0)/0x0(0)
  Last flood scan length is 0, maximum is 2
  Last flood scan time is 0 msec, maximum is 1 msec
  Neighbor Count is 2, Adjacent neighbor count is 2 
    Adjacent with neighbor 2.2.2.2
    Adjacent with neighbor 3.3.3.3  (Designated Router)
  Suppress hello for 0 neighbor(s)
R1#
You are now connected to R2. Use the show ip ospf interface g0/0/0 command to verify that R2 is a DROTHER.
R2#show ip ospf interface g0/0/0
GigabitEthernet0/0/0 is up, line protocol is up 
  Internet Address 192.168.1.2/24, Area 0, Attached via Interface Enable
  Process ID 10, Router ID 2.2.2.2, Network Type BROADCAST, Cost: 1
  Topology-MTID    Cost    Disabled    Shutdown      Topology Name
        0           1         no          no            Base
  Enabled by interface config, including secondary ip addresses
  Transmit Delay is 1 sec, State DROTHER, Priority 0
  Designated Router (ID) 3.3.3.3, Interface address 192.168.1.3
  Backup Designated router (ID) 1.1.1.1, Interface address 192.168.1.1
  Timer intervals configured, Hello 10, Dead 40, Wait 40, Retransmit 5
    oob-resync timeout 40
    Hello due in 00:00:03
  Supports Link-local Signaling (LLS)
  Cisco NSF helper support enabled
  IETF NSF helper support enabled
  Index 1/1, flood queue length 0
  Next 0x0(0)/0x0(0)
  Last flood scan length is 1, maximum is 2
  Last flood scan time is 0 msec, maximum is 0 msec
  Neighbor Count is 2, Adjacent neighbor count is 2 
    Adjacent with neighbor 1.1.1.1  (Backup Designated Router)
    Adjacent with neighbor 3.3.3.3  (Designated Router)
  Suppress hello for 0 neighbor(s)
R2#
You are now connected to R3. Use the show ip ospf interface g0/0/0 command to verify that R3 is the DR.
R3#show ip ospf interface g0/0/0
GigabitEthernet0/0/0 is up, line protocol is up 
  Internet Address 192.168.1.3/24, Area 0, Attached via Interface Enable
  Process ID 10, Router ID 3.3.3.3, Network Type BROADCAST, Cost: 1
  Topology-MTID    Cost    Disabled    Shutdown      Topology Name
        0           1         no          no            Base
  Enabled by interface config, including secondary ip addresses
  Transmit Delay is 1 sec, State DR, Priority 100
  Designated Router (ID) 3.3.3.3, Interface address 192.168.1.3
  Backup Designated router (ID) 1.1.1.1, Interface address 192.168.1.1
  Timer intervals configured, Hello 10, Dead 40, Wait 40, Retransmit 5
    oob-resync timeout 40
    Hello due in 00:00:00
  Supports Link-local Signaling (LLS)
  Cisco NSF helper support enabled
  IETF NSF helper support enabled
  Index 1/1/1, flood queue length 0
  Next 0x0(0)/0x0(0)/0x0(0)
  Last flood scan length is 1, maximum is 3
  Last flood scan time is 0 msec, maximum is 0 msec
  Neighbor Count is 2, Adjacent neighbor count is 2 
    Adjacent with neighbor 1.1.1.1  (Backup Designated Router)
    Adjacent with neighbor 2.2.2.2
  Suppress hello for 0 neighbor(s)
R3#
You have successfully modified the OSPF priority.
✓ You are connected to R2:
• Use the lo0 interface to set the loopback interface cost to 10
• Return to global configuration mode
• Verify the routing table entries with the show ip route ospf command
R2(config)#interface lo0
R2(config-if)#ip ospf cost 10
R2(config-if)#end
R2#show ip route ospf
(output omitted)
Gateway of last resort is not set
      10.0.0.0/8 is variably subnetted, 9 subnets, 3 masks
O        10.1.1.12/30 [110/20] via 10.1.1.10, 00:01:13, GigabitEthernet0/0/1
O        10.10.1.0/24 [110/20] via 10.1.1.5, 00:00:32, GigabitEthernet0/0/0
O        10.10.3.0/24 [110/11] via 10.1.1.10, 00:00:49, GigabitEthernet0/0/1
R2#
The cost value for R3’s local network is 11 because the loopback still reports a default cost of 1.
✓ You are now connected to R3:
• Use the lo0 interface and set the loopback interface cost to 10
• Use the g0/0/0 interface and set the link cost to R1 to 30
• Return to privileged EXEC mode
• Verify the routing table entries with the show ip route ospf command
R3(config)#interface lo0
R3(config-if)#ip ospf cost 10
R3(config-if)#interface g0/0/0
R3(config-if)#ip ospf cost 30
R3(config-if)#end
R3#show ip route ospf
(output omitted)
Gateway of last resort is not set
      10.0.0.0/8 is variably subnetted, 9 subnets, 3 masks
O        10.1.1.4/30 [110/20] via 10.1.1.9, 01:48:54, GigabitEthernet0/0/1
O        10.10.1.0/24 [110/30] via 10.1.1.9, 00:00:06, GigabitEthernet0/0/1
O        10.10.2.0/24 [110/20] via 10.1.1.9, 00:35:24, GigabitEthernet0/0/1
R3#
You have successfully modified the OSPF cost values for R2 and R3.
You are connected to R3. Enter the show ip ospf neighbor command to see that no adjacency currently exists with R1 and R2.
R3#show ip ospf neighbor
R3#
No output is returned for adjacent neighbors.
✓ You are now in global configuration mode:
• Use g0/0/0 as the interface name and configure the Hello interval to match R1
• Use g0/0/1 as the interface name and configure the Hello interval to match R2
• Return to privileged EXEC mode
• Verify that neighbor adjacencies are re-established with the show ip ospf neighbor command
R3(config)#interface g0/0/0
R3(config-if)#ip ospf hello-interval 5
*Jun  7 05:11:34.423: %OSPF-5-ADJCHG: Process 10, Nbr 1.1.1.1 on GigabitEthernet0/0/0 from LOADING to FULL, Loading Done
R3(config-if)#interface g0/0/1
R3(config-if)#ip ospf hello-interval 5
*Jun  7 05:11:43.081: %OSPF-5-ADJCHG: Process 10, Nbr 2.2.2.2 on GigabitEthernet0/0/1 from LOADING to FULL, Loading Done
R3(config-if)#end
R3#show ip ospf neighbor
Neighbor ID     Pri   State           Dead Time   Address         Interface
2.2.2.2           0   FULL/  -        00:00:19    10.1.1.9        GigabitEthernet0/0/1
1.1.1.1           0   FULL/  -        00:00:19    10.1.1.14       GigabitEthernet0/0/0
R3#
You have successfully modified the OSPF Hello and Dead intervals on R3.
Display a summary of the IPv4 interface status on R2.
R2#show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0/0   10.1.1.6        YES NVRAM  up                    up      
GigabitEthernet0/0/1   10.1.1.9        YES NVRAM  up                    up      
Serial0/1/0            unassigned      YES NVRAM  administratively down down    
Serial0/1/1            unassigned      YES NVRAM  administratively down down    
GigabitEthernet0       unassigned      YES NVRAM  administratively down down    
Loopback0              10.10.2.1       YES NVRAM  up                    up      
Loopback1              64.100.0.1      YES NVRAM  up                    up      
R2#
Display the OSPF routes installed in the routing table on R2.
R2#show ip route ospf
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area 
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2
       i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
       ia - IS-IS inter area, * - candidate default, U - per-user static route
       o - ODR, P - periodic downloaded static route, H - NHRP, l - LISP
       a - application route
       + - replicated route, % - next hop override
Gateway of last resort is 0.0.0.0 to network 0.0.0.0
      10.0.0.0/8 is variably subnetted, 9 subnets, 3 masks
O        10.1.1.12/30 [110/40] via 10.1.1.10, 00:45:28, GigabitEthernet0/0/1
                      [110/40] via 10.1.1.5, 00:45:49, GigabitEthernet0/0/0
O        10.10.1.0/24 [110/20] via 10.1.1.5, 00:45:49, GigabitEthernet0/0/0
O        10.10.3.0/24 [110/20] via 10.1.1.10, 00:45:28, GigabitEthernet0/0/1
R2#
Display the OSPF neighbor table for R2.
R2#show ip ospf neighbor
Neighbor ID     Pri   State           Dead Time   Address         Interface
3.3.3.3           0   FULL/  -        00:00:16    10.1.1.10       GigabitEthernet0/0/1
1.1.1.1           0   FULL/  -        00:00:19    10.1.1.5        GigabitEthernet0/0/0
R2#
Verify the protocol settings on R2.
R2#show ip protocols
***IP Routing is NSF aware***
(output omitted)
Routing Protocol is "ospf 10"
  Outgoing update filter list for all interfaces is not set
  Incoming update filter list for all interfaces is not set
  Router ID 2.2.2.2
  It is an autonomous system boundary router
 Redistributing External Routes from,
  Number of areas in this router is 1. 1 normal 0 stub 0 nssa
  Maximum path: 4
  Routing for Networks:
  Routing on Interfaces Configured Explicitly (Area 0):
    Loopback0
    GigabitEthernet0/0/1
    GigabitEthernet0/0/0
  Routing Information Sources:
    Gateway         Distance      Last Update
    3.3.3.3              110      00:46:14
    1.1.1.1              110      00:46:36
  Distance: (default is 110)
R2#
Verify the OSPF process on R2.
R2#show ip ospf
Routing Process "ospf 10" with ID 2.2.2.2
 Start time: 00:01:54.811, Time elapsed: 00:48:04.766
 Supports only single TOS(TOS0) routes
 Supports opaque LSA
 Supports Link-local Signaling (LLS)
 Supports area transit capability
 Supports NSSA (compatible with RFC 3101)
 Event-log enabled, Maximum number of events: 1000, Mode: cyclic
 It is an autonomous system boundary router
 Redistributing External Routes from,
 Router is not originating router-LSAs with maximum metric
 Initial SPF schedule delay 5000 msecs
 Minimum hold time between two consecutive SPFs 10000 msecs
 Maximum wait time between two consecutive SPFs 10000 msecs
 Incremental-SPF disabled
 Minimum LSA interval 5 secs
 Minimum LSA arrival 1000 msecs
 LSA group pacing timer 240 secs
 Interface flood pacing timer 33 msecs
 Retransmission pacing timer 66 msecs
 Number of external LSA 1. Checksum Sum 0x009F01
 Number of opaque AS LSA 0. Checksum Sum 0x000000
 Number of DCbitless external and opaque AS LSA 0
 Number of DoNotAge external and opaque AS LSA 0
 Number of areas in this router is 1. 1 normal 0 stub 0 nssa
 Number of areas transit capable is 0
 External flood list length 0
 IETF NSF helper support enabled
 Cisco NSF helper support enabled
 Reference bandwidth unit is 10000 mbps
    Area BACKBONE(0)
        Number of interfaces in this area is 3
	Area has no authentication
	SPF algorithm last executed 00:47:04.655 ago
	SPF algorithm executed 5 times
	Area ranges are
	Number of LSA 3. Checksum Sum 0x00E181
	Number of opaque link LSA 0. Checksum Sum 0x000000
	Number of DCbitless LSA 0
	Number of indication LSA 0
	Number of DoNotAge LSA 0
	Flood list length 0
R2#
Use the g0/0/0 interface to verify the OSPF interface settings on R2.
R2#show ip ospf interface g0/0/0
GigabitEthernet0/0/0 is up, line protocol is up 
  Internet Address 10.1.1.6/30, Area 0, Attached via Interface Enable
  Process ID 10, Router ID 2.2.2.2, Network Type POINT_TO_POINT, Cost: 10
  Topology-MTID    Cost    Disabled    Shutdown      Topology Name
        0           10        no          no            Base
  Enabled by interface config, including secondary ip addresses
  Transmit Delay is 1 sec, State POINT_TO_POINT
  Timer intervals configured, Hello 5, Dead 20, Wait 20, Retransmit 5
    oob-resync timeout 40
    Hello due in 00:00:02
  Supports Link-local Signaling (LLS)
  Cisco NSF helper support enabled
  IETF NSF helper support enabled
  Index 2/2, flood queue length 0
  Next 0x0(0)/0x0(0)
  Last flood scan length is 1, maximum is 1
  Last flood scan time is 0 msec, maximum is 1 msec
  Neighbor Count is 1, Adjacent neighbor count is 1 
    Adjacent with neighbor 1.1.1.1
  Suppress hello for 0 neighbor(s)
R2#
Display summary information for all OSPF interfaces on R2.
R2#show ip ospf interface brief
Interface    PID   Area            IP Address/Mask    Cost  State Nbrs F/C
Lo0          10    0               10.10.2.1/24       10    P2P   0/0
Gi0/0/1      10    0               10.1.1.9/30        10    P2P   1/1
Gi0/0/0      10    0               10.1.1.6/30        10    P2P   1/1
R2#
You are now connected to R3. Display a summary of the IPv4 interface status on R2.
R3#show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0/0   10.1.1.13       YES NVRAM  up                    up      
GigabitEthernet0/0/1   10.1.1.10       YES NVRAM  up                    up      
Serial0/1/0            unassigned      YES NVRAM  administratively down down    
Serial0/1/1            unassigned      YES NVRAM  administratively down down    
GigabitEthernet0       unassigned      YES NVRAM  administratively down down    
Loopback0              10.10.3.1       YES NVRAM  up                    up      
R3#
Display the OSPF routes installed in the routing table on R3.
R3#show ip route ospf
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area 
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2
       i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
       ia - IS-IS inter area, * - candidate default, U - per-user static route
       o - ODR, P - periodic downloaded static route, H - NHRP, l - LISP
       a - application route
       + - replicated route, % - next hop override, p - overrides from PfR
Gateway of last resort is 10.1.1.9 to network 0.0.0.0
O*E2  0.0.0.0/0 [110/1] via 10.1.1.9, 00:49:56, GigabitEthernet0/0/1
      10.0.0.0/8 is variably subnetted, 9 subnets, 3 masks
O        10.1.1.4/30 [110/20] via 10.1.1.9, 00:49:56, GigabitEthernet0/0/1
O        10.10.1.0/24 [110/30] via 10.1.1.9, 00:49:56, GigabitEthernet0/0/1
O        10.10.2.0/24 [110/20] via 10.1.1.9, 00:49:56, GigabitEthernet0/0/1
R3#
Display the neighbor table for R3.
R3#show ip ospf neighbor
Neighbor ID     Pri   State           Dead Time   Address         Interface
2.2.2.2           0   FULL/  -        00:00:18    10.1.1.9        GigabitEthernet0/0/1
1.1.1.1           0   FULL/  -        00:00:19    10.1.1.14       GigabitEthernet0/0/0
R3#
Afficher la table des voisins pour R3.
R3#show ip protocols
***IP Routing is NSF aware***
(output omitted)
Routing Protocol is "ospf 10"
  Outgoing update filter list for all interfaces is not set
  Incoming update filter list for all interfaces is not set
  Router ID 3.3.3.3
  Number of areas in this router is 1. 1 normal 0 stub 0 nssa
  Maximum path: 4
  Routing for Networks:
  Routing on Interfaces Configured Explicitly (Area 0):
    Loopback0
    GigabitEthernet0/0/1
    GigabitEthernet0/0/0
  Routing Information Sources:
    Gateway         Distance      Last Update
    1.1.1.1              110      00:50:44
    2.2.2.2              110      00:50:44
  Distance: (default is 110)
R3#
Verify the OSPF process on R3.
R3#show ip ospf
Routing Process "ospf 10" with ID 3.3.3.3
 Start time: 00:01:38.093, Time elapsed: 00:52:05.897
 Supports only single TOS(TOS0) routes
 Supports opaque LSA
 Supports Link-local Signaling (LLS)
 Supports area transit capability
 Supports NSSA (compatible with RFC 3101)
 Supports Database Exchange Summary List Optimization (RFC 5243)
 Event-log enabled, Maximum number of events: 1000, Mode: cyclic
 Router is not originating router-LSAs with maximum metric
 Initial SPF schedule delay 5000 msecs
 Minimum hold time between two consecutive SPFs 10000 msecs
 Maximum wait time between two consecutive SPFs 10000 msecs
 Incremental-SPF disabled
 Minimum LSA interval 5 secs
 Minimum LSA arrival 1000 msecs
 LSA group pacing timer 240 secs
 Interface flood pacing timer 33 msecs
 Retransmission pacing timer 66 msecs
 EXCHANGE/LOADING adjacency limit: initial 300, process maximum 300
 Number of external LSA 1. Checksum Sum 0x009F01
 Number of opaque AS LSA 0. Checksum Sum 0x000000
 Number of DCbitless external and opaque AS LSA 0
 Number of DoNotAge external and opaque AS LSA 0
 Number of areas in this router is 1. 1 normal 0 stub 0 nssa
 Number of areas transit capable is 0
 External flood list length 0
 IETF NSF helper support enabled
 Cisco NSF helper support enabled
 Reference bandwidth unit is 10000 mbps
    Area BACKBONE(0)
        Number of interfaces in this area is 3
	Area has no authentication
	SPF algorithm last executed 00:51:04.059 ago
	SPF algorithm executed 4 times
	Area ranges are
	Number of LSA 3. Checksum Sum 0x00E181
	Number of opaque link LSA 0. Checksum Sum 0x000000
	Number of DCbitless LSA 0
	Number of indication LSA 0
	Number of DoNotAge LSA 0
	Flood list length 0
Use the g0/0/0 interface to verify the OSPF interface settings on R3.
R3#
R3#show ip ospf interface g0/0/0
GigabitEthernet0/0/0 is up, line protocol is up 
  Internet Address 10.1.1.13/30, Area 0, Attached via Interface Enable
  Process ID 10, Router ID 3.3.3.3, Network Type POINT_TO_POINT, Cost: 30
  Topology-MTID    Cost    Disabled    Shutdown      Topology Name
        0           30        no          no            Base
  Enabled by interface config, including secondary ip addresses
  Transmit Delay is 1 sec, State POINT_TO_POINT
  Timer intervals configured, Hello 5, Dead 20, Wait 20, Retransmit 5
    oob-resync timeout 40
    Hello due in 00:00:02
  Supports Link-local Signaling (LLS)
  Cisco NSF helper support enabled
  IETF NSF helper support enabled
  Index 1/2/2, flood queue length 0
  Next 0x0(0)/0x0(0)/0x0(0)
  Last flood scan length is 1, maximum is 1
  Last flood scan time is 0 msec, maximum is 0 msec
  Neighbor Count is 1, Adjacent neighbor count is 1 
    Adjacent with neighbor 1.1.1.1
  Suppress hello for 0 neighbor(s)
R3#
Display summary information for all OSPF interfaces on R3.
R3#show ip ospf interface brief
Interface    PID   Area            IP Address/Mask    Cost  State Nbrs F/C
Lo0          10    0               10.10.3.1/24       10    P2P   0/0
Gi0/0/1      10    0               10.1.1.10/30       10    P2P   1/1
Gi0/0/0      10    0               10.1.1.13/30       30    P2P   1/1
R3#
You have successfully verified single-area OSPFv2 on R2 and R3.



