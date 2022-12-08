Alexandre Aparecido Scrocaro Junior\
Atividade 4 - Firewall com iptables

# Introdução
Nesta atividade foi realizada a configuração de um firewall em um roteador linux em uma rede simulada no software gns3. A rede consiste em uma LAN com faixa de IPs 172.30.0.0/24, uma DMZ (zona desmilitarizada, é uma sub-rede que tem a funcionalidade de fazer uma 'interface' da rede local com a internet) possui faixa de IPs 10.10.10.0/24 e a internet com um host configurado com faixa de IPs 192.168.122.0/24

# Definições

## Firewall
Funciona por meio de regras, que ditam o que entra e sai da rede e sua política que também é implementada por meio das regras, mas não analisa o pacote mais profundamente - o que deve ser feito pelo switch. É utilizado para isolar a rede de um ambiente hostil, como a internet.

Tem dois tipos de política:
- Liberar tudo:\
  Tudo que não é bloqueado por meio das regras será liberado.

- Bloquear tudo:\
  Bloqueia tudo que não é liberado por meio de regras.\
  Tende a ser mais seguro.
  
Projetos de firewall:
- Host screened:\
Não pode ser acessado como servidor.

- Host bastion:\
Pode ser acessado como servidor, mas somente para os serviços que ele propõe.

- Demilitarized zone (DMZ):\
Serve como uma espécie de interface da rede com a internet, é uma sub-rede que controla alguns serviços como servidor HTTP.

## Iptables
É o firewall do linux. Utilizado para configurar as regras do firewall, filtra serviços. Possui módulos como o `state` que controla conexões, `multiport` que permite a utilização de várias portas (protolos) na mesma regra ou `tcp-flags` que controla as flags SYN,ACK dos serviços que usam tcp.

## Tabelas

### Filter
Tabela do netfilter, filtra pacotes.

#### INPUT
Quando o firewall é o destino final do pacote.

#### OUTPUT
Quando o firewall é a origem do pacote.

#### FORWARD
Quando o firewall não é o destino final nem a origem, o pacote apenas passa por ele.


### Nat
Implementa funções de NAT.

#### OUTPUT
Quando o firewall é a origem do pacote.

#### PREROUTING
Alterações no pacote antes que ele seja roteado. Isso pode ocorrer em um redirecionamento como no exemplo abaixo.
```sh
# redireciona acesso HTTP vindo da internet para o host 3
echo "Libera/redireciona o acesso de máquinas da internet para a porta 80 do host 3" 
iptables -t nat -A PREROUTING -p tcp --dport 80 -i eth0 -j DNAT --to 10.10.10.3 
```

#### POSTROUTING
Alterações no pacote depois do tratamento de roteamento. Isso pode ocorrer para mascarar os ips da rede local para navegar na internet como no exemplo abaixo.
```sh
echo "Mascaramento"
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE 
```

### Mangle
Alterações especiais mais complexas em pacotes, como alterar a prioridade de entrada e saída de dele baseado no tipo de serviço que se destinava.

#### OUTPUT
Quando o firewall é a origem do pacote. Altera pacotes de forma especial antes que sejam roteados.

#### PREROUTING
Alterações no pacote antes que ele seja roteado.

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

#### Teste das configurações
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

## Configuração inicial do Firewall
```bash
# Criacao de seu arquivo de configuracao dentro do diretorio '/etc'
root@Firewall:/$ mkdir /etc/firewall
root@Firewall:/$ cd /etc/firewall
root@Firewall:/etc/firewall$ vi firewall.sh

# Dando permissoes no arquivo
root@Firewall:/etc/firewall$ chmod a+x firewall.sh
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
```
## Testes
### 1. Verificar se o Host 1 acessa o Host 3 via HTTP – ele deve conseguir.

Consegue por conta da regra F.\
![image](https://user-images.githubusercontent.com/37521313/206322187-e7118abb-baf7-4c4b-9989-1635c74234fe.png)

### 2. Verificar se o Host 1 acessa o Host 4 via HTTP – ele não deve conseguir.

Não consegue por conta da regra B.\
![image](https://user-images.githubusercontent.com/37521313/206322231-03fe52d1-4c19-47f3-b18d-74d7d6921990.png)

### 3. Verificar se o Host 1 acessa o Host 4 via HTTPS – ele deve conseguir.

Consegue por conta da regra G.\
![image](https://user-images.githubusercontent.com/37521313/206322302-6a713c6e-6f66-4fd0-b4ea-b200c9c993ff.png)

### 4. Verificar se o Host 2 acessa o Host 3 via HTTP, HTTPS e SSH – ele não deve conseguir.

Consegue por conta da regra F.\
Acessa via HTTP:\
![image](https://user-images.githubusercontent.com/37521313/206322378-8a31e77d-1b3b-4532-84aa-54d27ef9a034.png)

Não consegue por conta da regra F.\
Não acessa via HTTPS:\
![image](https://user-images.githubusercontent.com/37521313/206322512-31b9b3c2-876d-40dd-9c81-886604b261aa.png)

Consegue por conta da regra E.\
Acessa via SSH:\
![image](https://user-images.githubusercontent.com/37521313/206322553-e14e2d51-cd21-47ee-aaf3-abb3fc499cb2.png)

### 5. Verificar se o Host 2 acessa o Host 5 via SSH – ele deve conseguir.

Consegue por que nada o impede (politica de ACCEPT).\
![image](https://user-images.githubusercontent.com/37521313/206322599-5ffb6322-f9f8-4dad-9615-ba19ac0d307c.png)

### 6. Verificar se o Host 2 acessa o Host 1 via SSH – ele não deve conseguir.

Consegue por que nada o impede (politica de ACCEPT).\
Acessa via SSH:\
![image](https://user-images.githubusercontent.com/37521313/206322663-90a75852-90b0-443d-9421-49449c6ce9e1.png)

### 7. Verificar se o Host 1 acessa o Host 5 via HTTP, HTTPS e SSH – ele deve conseguir.

Consegue por que nada o impede (politica de ACCEPT).\
Acessa via HTTP:\
![image](https://user-images.githubusercontent.com/37521313/206322810-4c538d46-d878-4fd2-b4db-33393d7597f3.png)

Acessa via HTTPS:\
![image](https://user-images.githubusercontent.com/37521313/206322983-dec662d0-9f86-45df-8d23-ea5da6496418.png)

Acessa via SSH:\
![image](https://user-images.githubusercontent.com/37521313/206323013-e5901dce-870b-4ba9-b24a-809558575009.png)

### 8. Verificar se o Host 5 acessa o Host 3 via HTTP - ele deve conseguir.

Consegue por que nada o impede (politica de ACCEPT).\
![image](https://user-images.githubusercontent.com/37521313/206323091-bfdd438f-ee77-464d-8b29-17c3a979a9d7.png)

### 9. Verificar se o Host 5 acessa o Host 3 via HTTPS, Telnet e SSH - ele não deve conseguir.

Não consegue por conta da regra F.\
Nao acessa via HTTPS:\
![image](https://user-images.githubusercontent.com/37521313/206323144-e18e38d9-0331-455e-91bc-67afeded45d8.png)

Nao acessa via Telnet:\
![image](https://user-images.githubusercontent.com/37521313/206323217-5a604fcc-e892-4d9a-aedc-2d0f19909544.png)

Nao acessa via SSH:\
![image](https://user-images.githubusercontent.com/37521313/206323249-560fbaf6-f131-4d12-8791-8e2d73fdc0b2.png)

### 10. Verificar se o Host 5 acessa o Host 4 via HTTP e HTTPS - ele deve conseguir.

Consegue por que nada o impede (politica de ACCEPT) + regra G.\
Acessa via HTTP:\
![image](https://user-images.githubusercontent.com/37521313/206323302-5092b894-cd8e-4fc4-8eea-2c108c453d85.png)

Acessa via HTTPS:\
![image](https://user-images.githubusercontent.com/37521313/206323344-c4a9d819-031b-4ffc-9266-7818464affae.png)

### 11. Verificar se o Host 5 acessa o Host 4 via MYSQL - ele não deve conseguir.

Não consegue por conta da regra H.\
![image](https://user-images.githubusercontent.com/37521313/206323378-37ad4967-4181-451d-8213-66078198a482.png)

### 12. Verificar se o Host 5 acessa o Host 1 via HTTP e HTTPS - ele não deve conseguir.

Não consegue por conta da regra I.\
Nao acessa via HTTP:\
![image](https://user-images.githubusercontent.com/37521313/206323547-fa2c734c-2a32-49bd-bfbd-da2b83b69cd7.png)

Nao acessa via HTTPS:\
![image](https://user-images.githubusercontent.com/37521313/206323593-98028c70-bbb7-4fd4-9a04-6badacf99a3d.png)

### 13. Verificar se o Host 1 acessa o Firewall via SSH - ele deve conseguir.

Consegue por conta da regra D.\
![image](https://user-images.githubusercontent.com/37521313/206323752-0da40108-bdd5-46a2-a069-105239cd20cd.png)

![image](https://user-images.githubusercontent.com/37521313/206323795-4613c63f-a903-4598-aa56-4c4e19dc8aea.png)

![image](https://user-images.githubusercontent.com/37521313/206323834-31c37d33-83a2-44b9-9299-27b0c50bd7a0.png)

### 14. Verificar se o Host 1 acessa o Firewall via HTTP, HTTPS e MYSQL - ele não deve conseguir.

Não consegue por conta da regra D.\
Nao acessa via HTTP:\
![image](https://user-images.githubusercontent.com/37521313/206323935-7efe238a-88b6-4e85-9789-297fc29e6145.png)

Nao acessa via HTTPS:\
![image](https://user-images.githubusercontent.com/37521313/206324021-24390161-b044-4fa0-8edc-f07c972253a7.png)

Nao acessa via MYSQL:\
![image](https://user-images.githubusercontent.com/37521313/206324061-83b5c9ac-d3dd-4423-a914-7768d4b12a10.png)

### 15. Verificar se o Host 4 acessa o Firewall via SSH, Telnet, HTTP, HTTPS e MYSQL - ele não deve conseguir.

Não consegue por conta da regra D.\
Nao acessa via nenhum:\
![image](https://user-images.githubusercontent.com/37521313/206324429-c23324c6-06a3-4e18-b0de-69fb55aad0aa.png)

### 16. Verificar se o Host 5 acessa o Firewall via SSH, Telnet, HTTP, HTTPS e MYSQL - ele não deve conseguir.

Não consegue por conta da regra D.\
Nao acessa via nenhum:\
![image](https://user-images.githubusercontent.com/37521313/206324573-ab8ba293-f50e-4f45-837a-6be9f7e917d6.png)

### 17. Verificar se o Host 5 acessa o Host1 via SSH, Telnet, HTTP, HTTPS e MYSQL - ele não deve conseguir.

Não consegue por conta da regra I.\
Nao acessa via nenhum:\
![image](https://user-images.githubusercontent.com/37521313/206324748-bf7115ec-549d-435f-bba3-afd293a07e24.png)

### 18. Verificar se o Host 3 acessa o Host1 via SSH, Telnet, HTTP, HTTPS e MYSQL - ele não deve conseguir.

Não consegue por conta da regra I.\
Nao acessa via nenhum:\
![image](https://user-images.githubusercontent.com/37521313/206324820-1745c219-274e-4037-ab32-f96d89e5948a.png)


# Referências
Slides do professor Luiz Arthur Feitosa dos Santos, contidos no moodle da matéria.

