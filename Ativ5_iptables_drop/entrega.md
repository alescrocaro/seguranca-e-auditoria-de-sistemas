# Cenário

![image](https://user-images.githubusercontent.com/37521313/206291541-cf0735f3-63ef-4254-85ca-e8f6e804e3ad.png)

## Configuração da rede
#### LAN1:
Host 1:
```
auto eth0
iface eth0 inet static
  hwaddress 00:00:00:00:00:01
  address 172.30.0.1
  netmask 255.255.255.0
  gateway 172.30.0.254
  up echo nameserver 8.8.8.8 > /etc/resolv.conf

up /usr/bin/iperf3 -s -p 80 -D
up /usr/bin/iperf3 -s -p 443 -D
up /usr/bin/iperf3 -s -p 3306 -D
up /usr/bin/iperf3 -s -p 23 -D
up /usr/bin/iperf3 -s -p 22 -D
```

Host 2:
```
auto eth0
iface eth0 inet static
  hwaddress 00:00:00:00:00:02
  address 172.30.0.2
  netmask 255.255.255.0
  gateway 172.30.0.254
  up echo nameserver 8.8.8.8 > /etc/resolv.conf
  
up /usr/bin/iperf3 -s -p 80 -D
up /usr/bin/iperf3 -s -p 443 -D
up /usr/bin/iperf3 -s -p 3306 -D
up /usr/bin/iperf3 -s -p 23 -D
up /usr/bin/iperf3 -s -p 22 -D
```

#### DMZ:
Host 3:
```
auto eth0
iface eth0 inet static
  hwaddress 00:00:00:00:00:03
  address 10.10.10.3
  netmask 255.255.255.0
  gateway 10.10.10.254
  up echo nameserver 8.8.8.8 > /etc/resolv.conf
  
up /usr/bin/iperf3 -s -p 80 -D
up /usr/bin/iperf3 -s -p 443 -D
up /usr/bin/iperf3 -s -p 3306 -D
up /usr/bin/iperf3 -s -p 23 -D
up /usr/bin/iperf3 -s -p 22 -D
```

Host 4:
```
auto eth0
iface eth0 inet static
  hwaddress 00:00:00:00:00:04
  address 10.10.10.4
  netmask 255.255.255.0
  gateway 10.10.10.254
  up echo nameserver 8.8.8.8 > /etc/resolv.conf
  
up /usr/bin/iperf3 -s -p 80 -D
up /usr/bin/iperf3 -s -p 443 -D
up /usr/bin/iperf3 -s -p 3306 -D
up /usr/bin/iperf3 -s -p 23 -D
up /usr/bin/iperf3 -s -p 22 -D
```

#### Internet:
Host 5:
```
auto eth0
iface eth0 inet static
  hwaddress 00:00:00:00:00:05
  address 192.168.122.5
  netmask 255.255.255.0
  gateway 192.168.122.254
  up echo nameserver 8.8.8.8 > /etc/resolv.conf
  
up /usr/bin/iperf3 -s -p 80 -D
up /usr/bin/iperf3 -s -p 443 -D
up /usr/bin/iperf3 -s -p 3306 -D
up /usr/bin/iperf3 -s -p 23 -D
up /usr/bin/iperf3 -s -p 22 -D
```

#### Firewall:
```
auto eth0
iface eth0 inet static
  hwaddress 00:00:00:00:01:01
  address 192.168.122.254
  netmask 255.255.255.0
  gateway 192.168.122.1
  up echo nameserver 8.8.8.8 > /etc/resolv.conf
  
auto eth1
iface eth1 inet static
  hwaddress 00:00:00:00:01:02
  address 172.30.0.254
  netmask 255.255.255.0
  
auto eth2
iface eth2 inet static
  hwaddress 00:00:00:00:01:03
  address 10.10.10.254
  netmask 255.255.255.0
  
  
up /usr/bin/iperf3 -s -p 80 -D
up /usr/bin/iperf3 -s -p 443 -D
up /usr/bin/iperf3 -s -p 3306 -D
up /usr/bin/iperf3 -s -p 23 -D
up /usr/bin/iperf3 -s -p 22 -D
```

## Criando regras do firewall
A: Com a política de liberar tudo em todas as situações.\
B: Proibir que o Host 1 acesse o serviço de HTTP no Host 4.\
C: Impedir que qualquer host conectado ao firewall acesse Telnet entre as redes.\
D: Somente o Host 1 pode acessar o firewall via SSH, fora isso ninguém deve acessar nenhum servidor no Firewall.\
E: Somente os hosts da LAN pode acessar a DMZ via SSH.\
F: O Host 3 só pode ser acessado como servidor HTTP, de qualquer rede.\
G: O Host 4 só pode ser acessado como servidor HTTP/HTTPS, de qualquer rede.\
H: A DMZ não pode ser acessada via MYSQL.\
I: A LAN deve ser configurada como LAN Screened.

```sh
echo "Iniciando firewall"

echo "LIMPANDO TABELAS"
iptables -F
iptables -t nat -F
iptables -t mangle -F

echo "HABILITAR ROTEAMENTO"
echo 1 > /proc/sys/net/ipv4/ip_forward

echo "MASCARAMENTO"
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

echo "POLITICA DE DROP"
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP



echo "LAN screened"
iptables -A FORWARD -o eth1 -m state --state NEW,INVALID -j DROP

echo "LAN pode acessar qualquer servico"
#iptables -A FORWARD -i eth1 -j ACCEPT
#iptables -A FORWARD -o eth1 -j ACCEPT



echo "HOST 3 eh apenas servidor HTTP pra qualquer rede"
iptables -A FORWARD -p tcp --dport 80 -o eth2 -d 10.10.10.3 -j ACCEPT
iptables -A FORWARD -p tcp --sport 80 -s 10.10.10.3 -j ACCEPT



echo "HOST 4 eh servidor HTTPS e MYSQL pra qualquer rede"
iptables -A FORWARD -m multiport -p tcp --dport 443,3306 -d 10.10.10.4 -j ACCEPT
iptables -A FORWARD -m multiport -p tcp --sport 443,3306 -s 10.10.10.4 -j ACCEPT



echo "HOSTS da DMZ e FIREWALL soh podem ser clientes DNS, HTTP e HTTPS"
iptables -A FORWARD -m multiport -p tcp --dport 80,443 -i eth2 -j ACCEPT
iptables -A FORWARD -m multiport -p tcp --sport 80,443 -o eth2 -j ACCEPT

iptables -A FORWARD -p udp --dport 53 -i eth2 -j ACCEPT
iptables -A FORWARD -p udp --sport 53 -o eth2 -j ACCEPT

iptables -A OUTPUT -m multiport -p tcp --dport 80,443 -j ACCEPT
iptables -A INPUT -m multiport -p tcp --sport 80,443 -j ACCEPT 

iptables -A OUTPUT -p udp --dport 53 -j ACCEPT
iptables -A INPUT -p udp --sport 53 -j ACCEPT



echo "HOST 1 pode acessar firewall via ssh, mas controlado por MAC"
iptables -A INPUT -p tcp --dport 22 -i eth1 -m mac --mac-source 00:00:00:00:00:01 -j ACCEPT
iptables -A OUTPUT -p tcp --sport 22 -o eth1 -j ACCEPT 

echo "Configuracao concluida."
```
