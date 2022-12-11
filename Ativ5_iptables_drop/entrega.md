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
echo "Iniciando Firewall..."

echo "Limpa tabelas"
iptables -t nat -F
iptables -t mangle -F
iptables -F

echo 1 > /proc/sys/net/ipv4/ip_forward

# politica de liberar tudo eh padrao


echo "Proibe host1 de acessar servico de HTTP no host4"
iptables -A FORWARD -s 172.30.0.1 -d 10.10.10.4 -p tcp --dport 80 -j DROP


echo "Impede que qualquer host conectado ao firewall acesse telnet entre
as redes"
iptables -A FORWARD -p tcp --dport 23 -j DROP


echo "Somente host1 pode acessar firewall via ssh, fora isso ninguem pode 
acessar nenhum servidor no firewall"
iptables -A INPUT -s 172.30.0.1 -p tcp --dport 22 -j ACCEPT
iptables -A INPUT -m state --state NEW,INVALID -j DROP


echo "Somente hosts da LAN podem acessar DMZ via SSH"
iptables -A FORWARD -i eth1 -o eth2 -p tcp --dport 22 -j ACCEPT
iptables -A FORWARD -o eth2 -p tcp --dport 22 -j DROP


echo "host3 so pode ser acessado como servidor HTTP, de qualquer rede"
iptables -A FORWARD -d 10.10.10.3 -p tcp --dport 80 -j ACCEPT
iptables -A FORWARD -d 10.10.10.3 -j DROP


echo "host4 so pode ser acessado como servidor HTTP/HTTPS, de qualquer rede"
iptables -A FORWARD -d 10.10.10.4 -m multiport -p tcp --dport 80,443 -j ACCEPT
iptables -A FORWARD -d 10.10.10.4 -j DROP


echo "DMZ nao pode ser acessada via MYSQL"
iptables -A FORWARD -o eth2 -p tcp --dport 3306 -j DROP


echo "LAN deve ser configurada como host-screened"
iptables -A FORWARD -o eth1 -m state --state NEW,INVALID  -j DROP


echo "Configuracao concluida."
```## Criando regras do firewall
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
echo "Iniciando Firewall..."

echo "Limpa tabelas"
iptables -t nat -F
iptables -t mangle -F
iptables -F

echo 1 > /proc/sys/net/ipv4/ip_forward

# politica de liberar tudo eh padrao


echo "Proibe host1 de acessar servico de HTTP no host4"
iptables -A FORWARD -s 172.30.0.1 -d 10.10.10.4 -p tcp --dport 80 -j DROP


echo "Impede que qualquer host conectado ao firewall acesse telnet entre
as redes"
iptables -A FORWARD -p tcp --dport 23 -j DROP


echo "Somente host1 pode acessar firewall via ssh, fora isso ninguem pode 
acessar nenhum servidor no firewall"
iptables -A INPUT -s 172.30.0.1 -p tcp --dport 22 -j ACCEPT
iptables -A INPUT -m state --state NEW,INVALID -j DROP


echo "Somente hosts da LAN podem acessar DMZ via SSH"
iptables -A FORWARD -i eth1 -o eth2 -p tcp --dport 22 -j ACCEPT
iptables -A FORWARD -o eth2 -p tcp --dport 22 -j DROP


echo "host3 so pode ser acessado como servidor HTTP, de qualquer rede"
iptables -A FORWARD -d 10.10.10.3 -p tcp --dport 80 -j ACCEPT
iptables -A FORWARD -d 10.10.10.3 -j DROP


echo "host4 so pode ser acessado como servidor HTTP/HTTPS, de qualquer rede"
iptables -A FORWARD -d 10.10.10.4 -m multiport -p tcp --dport 80,443 -j ACCEPT
iptables -A FORWARD -d 10.10.10.4 -j DROP


echo "DMZ nao pode ser acessada via MYSQL"
iptables -A FORWARD -o eth2 -p tcp --dport 3306 -j DROP


echo "LAN deve ser configurada como host-screened"
iptables -A FORWARD -o eth1 -m state --state NEW,INVALID  -j DROP


echo "Configuracao concluida."
```
