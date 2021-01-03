# iptables-examples

making NAT rules in iptables:

see all the rules:

`iptables -t nat -v -L -n --line-number`

ssh port forwarding:

2020 is the new port that will forward the request to the 3022 of the destination host:

`iptables -t nat -A PREROUTING -p tcp --dport 2020 -j DNAT --to-destination 172.16.20.20:3022`

delete PREROUTING rules no.6

`iptables -t nat -D PREROUTING 6`

delete POSTROUTING rules no.7

`iptables -t nat -D POSTROUTING 7`

access internet from a host with private internet:

say your host is the gateway (172.16.20.1) and you want to allow traffic for 172.16.20.20:

`iptables -t nat -A POSTROUTING -s 172.16.20.20 -j MASQUERADE`

network issue on nodes, could ping the gateway bu couln’t access to the internet:

`cat /proc/sys/net/ipv4/ip_forward`
0

`echo 1 > /proc/sys/net/ipv4/ip_forward`

but it’s not permanent:

to make it permanent:

`sysctl net.ipv4.ip_forward
sysctl -w net.ipv4.ip_forward=1`
