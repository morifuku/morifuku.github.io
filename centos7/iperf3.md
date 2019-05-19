## IPv6 iperf3 Trial
A simple IPv6 traffic test by using iperf3 without IPv6 NDP procedure.
Real Programmers use iperf3 for the initial trial then make the REAL traffic generator by themselves.

### Client
Send packets from Client (2001:2::14) to Server (2001:3::19) via Gateway-Front (2001:2::12)
```
nmcli c mod eth0 ipv6.address 2001:2::14/64
nmcli c down eth0
nmcli c up eth0
ip -6 neigh add 2001:2::12 lladdr a0:36:9f:a3:5b:fe dev eth0
route add -A inet6 2001:3::19 gw 2001:2::12
iperf3 -u -c 2001:3::19 -b 900M
```

### Gateway
IP forward between Front (2001:2::12) and Rear (2001:3::12)
```
nmcli c mod enp1s0f0 ipv6.address 2001:2::12/64
nmcli c mod enp1s0f1 ipv6.address 2001:3::12/64
nmcli c down enp1s0f0 enp1s0f1
nmcli c up enp1s0f0
nmcli c up enp1s0f1
echo 1 > /proc/sys/net/ipv6/conf/all/forwarding
```

### Server
Receive packets from Client (2001:2::14) to Server (2001:3::19) via Gateway-Rear (2001:3::12)
```
nmcli c mod enp1s0f1 ipv6.address 2001:3::19/64
nmcli c down enp1s0f1
nmcli c up enp1s0f1
ip -6 neigh add 2001:3::12 lladdr a0:36:9f:a3:5b:ff dev enp1s0f1
route add -A inet6 2001:2::14 gw 2001:3::12
iperf3 -s

```
