"prueba ping a DNSA"
vagrant@bookworm:~$ ping 192.168.57.10
PING 192.168.57.10 (192.168.57.10) 56(84) bytes of data.
64 bytes from 192.168.57.10: icmp_seq=1 ttl=64 time=0.151 ms
64 bytes from 192.168.57.10: icmp_seq=2 ttl=64 time=0.117 ms
64 bytes from 192.168.57.10: icmp_seq=3 ttl=64 time=0.116 ms
64 bytes from 192.168.57.10: icmp_seq=4 ttl=64 time=0.165 ms
^C
--- 192.168.57.10 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3075ms
rtt min/avg/max/mdev = 0.116/0.137/0.165/0.021 ms

"prueba ping a DNSB"
vagrant@bookworm:~$ ping 192.168.57.11
PING 192.168.57.11 (192.168.57.11) 56(84) bytes of data.
64 bytes from 192.168.57.11: icmp_seq=1 ttl=64 time=0.277 ms
64 bytes from 192.168.57.11: icmp_seq=2 ttl=64 time=0.126 ms
64 bytes from 192.168.57.11: icmp_seq=3 ttl=64 time=0.112 ms
64 bytes from 192.168.57.11: icmp_seq=4 ttl=64 time=0.178 ms
^C
--- 192.168.57.11 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3078ms
rtt min/avg/max/mdev = 0.112/0.173/0.277/0.064 ms

"consulta del servidor DNS"
vagrant@bookworm:~$ dig @192.168.57.10 server01.informatica.ies.test

; <<>> DiG 9.18.28-1~deb12u2-Debian <<>> @192.168.57.10 server01.informatica.ies.test
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 7640
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: d73328880fa6932e0100000067312c40c521b74ca9314584 (good)
;; QUESTION SECTION:
;server01.informatica.ies.test. IN      A

;; ANSWER SECTION:
server01.informatica.ies.test. 86400 IN A       192.168.57.10

;; Query time: 0 msec
;; SERVER: 192.168.57.10#53(192.168.57.10) (UDP)
;; WHEN: Sun Nov 10 21:57:20 UTC 2024
;; MSG SIZE  rcvd: 102

"consulta de nombres"
vagrant@bookworm:~$ nslookup server01.informatica.ies.test 192.168.57.10
Server:         192.168.57.10
Address:        192.168.57.10#53

Name:   server01.informatica.ies.test
Address: 192.168.57.10

"consulta inversa"
vagrant@bookworm:~$ dig -x 192.168.57.10

; <<>> DiG 9.18.28-1~deb12u2-Debian <<>> -x 192.168.57.10
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 34337
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 674fe320ab93198d0100000067312cb2313ae6e6d7a88bd6 (good)
;; QUESTION SECTION:
;10.57.168.192.in-addr.arpa.    IN      PTR

;; AUTHORITY SECTION:
168.192.IN-ADDR.ARPA.   86400   IN      SOA     168.192.IN-ADDR.ARPA. . 0 28800 7200 604800 86400

;; Query time: 0 msec
;; SERVER: 192.168.57.10#53(192.168.57.10) (UDP)
;; WHEN: Sun Nov 10 21:59:14 UTC 2024
;; MSG SIZE  rcvd: 138

"verificacion del archivo de configuracion"
vagrant@bookworm:~$ cat /etc/resolv.conf
nameserver 192.168.57.10