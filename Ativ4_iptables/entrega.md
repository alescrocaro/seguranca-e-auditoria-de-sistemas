# Cenário

![image](https://user-images.githubusercontent.com/37521313/206291541-cf0735f3-63ef-4254-85ca-e8f6e804e3ad.png)

# Configuração da rede
### LAN1:
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

### DMZ:
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

### Internet:
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

### Firewall:
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

### Teste
Com as configurações de ips e gws prontas, deve-se então testar se as máquinas realizam pings entre si e se o iperf está funcionando corretamente. Para tanto, executa-se os seguintes comandos:

```bash
# pings
root@Host-1:/$ ping 172.30.0.2
root@Host-1:/$ ping 10.10.10.4
root@Host-1:/$ ping 192.168.122.5

# serviços (teste também para o host 192.168.122.5)
root@Host-1:/$ iperf3 -c 10.10.10.3 -p 22
root@Host-1:/$ iperf3 -c 10.10.10.3 -p 23
root@Host-1:/$ iperf3 -c 10.10.10.3 -p 80
root@Host-1:/$ iperf3 -c 10.10.10.3 -p 443
root@Host-1:/$ iperf3 -c 10.10.10.3 -p 3306
```

# Configuração inicial do Firewall
```bash
# Criacao de seu arquivo de configuracao dentro do diretorio '/etc'
root@Firewall:/$ mkdir /etc/firewall
root@Firewall:/$ cd /etc/firewall
root@Firewall:/etc/firewall$ vi firewall.sh

# Dando permissoes no arquivo
root@Firewall:/etc/firewall$ chmod a+x firewall.sh
```

# Criando regras do firewall
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


echo "Impede que qualquer host conectado ao firewall acesse telnet entre as redes"
iptables -A FORWARD -p tcp --dport 23 -j DROP


echo "Somente host1 pode acessar firewall via ssh, fora isso ninguem pode acessar nenhum servidor no firewall"
iptables -A INPUT -s 172.30.0.1 -p tcp --dport 22 -j ACCEPT
iptables -A INPUT -m state --state NEW -j DROP


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

Erros que não consegui corrigir:\
4. host 2 consegue acessar host 3 via ssh, http, mas não consegue via https
6. host 2 consegue acessar host 1 via ssh.


