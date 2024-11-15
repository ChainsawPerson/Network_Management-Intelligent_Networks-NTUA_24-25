# EX3
docker / containerlab intro 

## part2 : 

### topology :
host1 (10.20.1.2) ---- (10.20.1.1) srl1  (.2.1) ---- (2.2) srl2 (.3.1) ---- (.3.2) host2
 
host : 
- docker exec -it clab-my-topology-host1  /bin/bash
- ifconfig eth1 10.20.1.2 netmask 255.255.255.0 mtu 9100
- route add -host 10.20.3.2 gw 10.20.1.1

router:
ssh 
- enter candidate
- set interface ethernet-1/1 admin-state enable
- set interface ethernet-1/1 mtu 9100
- set interface ethernet-1/1 subinterface 0 ipv4 address 10.20.1.1/24
- set interface ethernet-1/1 subinterface 0 ipv4 admin-state enable
- set network-instance default interface ethernet-1/1.0
- commit stay


BGP:
- set network-instance default protocols bgp autonomous-system 20001
- set network-instance default protocols bgp router-id 10.20.2.1
- set network-instance default protocols bgp afi-safi ipv4-unicast admin-state enable
- set network-instance default protocols bgp group spine-underlay peer-as 20002
- set network-instance default protocols bgp group spine-underlay export-policy [direct-only]
- set network-instance default protocols bgp group spine-underlay import-policy [bgp-only]
- set network-instance default protocols bgp neighbor 10.20.2.2 peer-group spine-underlay
- set routing-policy policy direct-only default-action policy-result reject
- set routing-policy policy direct-only statement direct-routes-only match protocol local
- set routing-policy policy direct-only statement direct-routes-only action policy-result accept
- set routing-policy policy bgp-only default-action policy-result reject
- set routing-policy policy bgp-only statement bgp-routes-only match protocol bgp
- set routing-policy policy bgp-only statement bgp-routes-only action policy-result accept




