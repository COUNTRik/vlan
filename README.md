# VLAN и BOND

Запустить стенд *vagrant up* (*provision.yml* установит необходимые пакеты и включит forward).
После запустим *vlan.yml*, который скопирует конфиши и перезапустит network service.

## BOND

	[root@centralRouter vagrant]# ip addr show bond0 
	6: bond0: <BROADCAST,MULTICAST,MASTER,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
	    link/ether 08:00:27:91:00:e3 brd ff:ff:ff:ff:ff:ff
	    inet 192.168.255.2/24 brd 192.168.255.255 scope global bond0
	       valid_lft forever preferred_lft forever
	    inet6 fe80::a00:27ff:fe91:e3/64 scope link 
	       valid_lft forever preferred_lft forever
	[root@centralRouter vagrant]# ping -c 3 192.168.255.1 
	PING 192.168.255.1 (192.168.255.1) 56(84) bytes of data.
	64 bytes from 192.168.255.1: icmp_seq=1 ttl=64 time=0.585 ms
	64 bytes from 192.168.255.1: icmp_seq=2 ttl=64 time=0.665 ms
	64 bytes from 192.168.255.1: icmp_seq=3 ttl=64 time=0.660 ms

	--- 192.168.255.1 ping statistics ---
	3 packets transmitted, 3 received, 0% packet loss, time 2001ms
	rtt min/avg/max/mdev = 0.585/0.636/0.665/0.046 ms

## VLAN

*vlan100*

	[root@testClient1 vagrant]# ip addr show vlan100      
	4: vlan100@eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
	    link/ether 08:00:27:5d:fe:25 brd ff:ff:ff:ff:ff:ff
	    inet 10.10.10.1/24 brd 10.10.10.255 scope global vlan100
	       valid_lft forever preferred_lft forever
	    inet6 fe80::a00:27ff:fe5d:fe25/64 scope link 
	       valid_lft forever preferred_lft forever
	[root@testClient1 vagrant]# ping -c 3 10.10.10.254
	PING 10.10.10.254 (10.10.10.254) 56(84) bytes of data.
	64 bytes from 10.10.10.254: icmp_seq=1 ttl=64 time=1.99 ms
	64 bytes from 10.10.10.254: icmp_seq=2 ttl=64 time=0.638 ms
	64 bytes from 10.10.10.254: icmp_seq=3 ttl=64 time=0.666 ms

	--- 10.10.10.254 ping statistics ---
	3 packets transmitted, 3 received, 0% packet loss, time 2001ms
	rtt min/avg/max/mdev = 0.638/1.099/1.993/0.632 ms

*vlan101*

	[vagrant@testClient2 ~]$ ip addr show vlan101
	4: vlan101@eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
	    link/ether 08:00:27:65:1b:69 brd ff:ff:ff:ff:ff:ff
	    inet 10.10.10.1/24 brd 10.10.10.255 scope global vlan101
	       valid_lft forever preferred_lft forever
	    inet6 fe80::a00:27ff:fe65:1b69/64 scope link 
	       valid_lft forever preferred_lft forever
	[vagrant@testClient2 ~]$ ping -c 3 10.10.10.254
	PING 10.10.10.254 (10.10.10.254) 56(84) bytes of data.
	64 bytes from 10.10.10.254: icmp_seq=1 ttl=64 time=0.952 ms
	64 bytes from 10.10.10.254: icmp_seq=2 ttl=64 time=0.610 ms
	64 bytes from 10.10.10.254: icmp_seq=3 ttl=64 time=0.661 ms

	--- 10.10.10.254 ping statistics ---
	3 packets transmitted, 3 received, 0% packet loss, time 2003ms
	rtt min/avg/max/mdev = 0.610/0.741/0.952/0.150 ms
