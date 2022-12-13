# VPN - Virtual Private Network

* VPN cria túneis virtuais de comunicação entre redes ou hosts, trafegando os dados de forma segura usando criptografia para aumentar a transferencia de dados
* Lembrar de empresas com matriz e filiais
  * ao invés de manter uma rede privada (LAN), a empresa terá uma rede ainda privada só que como uma MAN ou WAN e o custo para manter uma rede empresarial deste porte vai se tornar rapidamente muito caro
  * a solução para isso é a VPN, que vai ligar a rede da matriz e filiais por meio de uma rede pública como a internet, com os dados sendo transmitidos por uma VPN
* Outro problema tratado por VPNs é que a internet trabalha com protocolos TCP/IP, mas algumas LANs não, o encapsulamento irá possibilitar ligar redes q n usam TCP/IP com a internet
* O termo Virtual entra, porque depende de uma conexão virtual, temporária, sem presença física no meio. Essa conexão virtual consiste em troca de pacotes, sendo roteados entre vários equipamentos
![image](https://user-images.githubusercontent.com/37521313/206934323-51933463-a45b-41c1-9610-56f469a783f6.png)

![image](https://user-images.githubusercontent.com/37521313/206934332-b15e5d9e-7809-4d4a-8004-bf2ed0e5ca80.png)

![image](https://user-images.githubusercontent.com/37521313/206934343-2901afa9-2265-47d0-a1b7-cd9e02ea8360.png)

este último é o típico caso de ligações entre filiais e matriz, formando uma **extranet**. Cabe ao gateway da VPN definir quais usuários irão trafegar pela Internet e, dentre estes, quais irão usar o túnel VPN. Neste caso a VPN é totalmente transparente para os usuários da rede. Neste caso os dados criptografados só ocorre entre os GWs e n dentro das LANs


![image](https://user-images.githubusercontent.com/37521313/206934439-825da57c-13f0-4000-be2f-4edf508fea04.png)

Este é um cenário híbrido no qual temos hosts de acesso isolado (não permanentes) aos gateways da VPN, e outra conexão permanente entre os gateways VPN.


## Segurança
* VPN Mantém privacidade, integridade e autenticidade da info que trafega através da rede pública
* Nenhum equipamento nem ninguém da rede pública pode conseguir ler os dados, para tanto pode:
  * Adquirir uma infra-estrutura física de rede fornecida por uma empresa 
  * Ou Usar criptografia p impossibilitar a compreensão da info por pessoas n autorizadas

### Criptografia
* Chaves simétricas
  * mesmo segredo compartilhado por todos
  * similar a chave única
  * emissor e destinatário devem esconder a chave de outras pessoas
  * ótimo desempenho em relação à outras técnicas

* Chaves assimétricas
  * tbm chamadas de chaves públicas
  * similar a chave publica privada
  * 2 chaves:
    * Uma privada e única p o usuário q n pode ser compartilhada com ngm
    * outra de domínio público e disseminada p qlqr pessoa que deseja enviar dados criptografados
  * desvantagem: se preocupa muito com a criptografia e não com a autenticação do usuário        

* RSA
  * muito lento

* Encapsulamento e protocolos
  * comparacao com carta
    * imagine uma carta com conteudo q contem os dados de destinatário e remetente mas n ta nos padroes do correio
    * tal carta eh colocada dentro de outro envelope com os padroes corretos
  * se uma rede n tem TCP IP, para trafegar na internet por ela, coloca o pacote dentro de um pacote IP p conseguir trafegar
  * O encapsulamento consiste em gerar um novo cabeçalho com o datagrama original como payload
  * Já o protocolo define quais métodos criptograficos sao usados, como o pacote sera encapsulado


## Anotações
Tunelamento -> Trafegar dados de uma rede privada em uma rede pública, mas pode ser feito priv-priv ou pub-pub\
nat - qnd o pacote sai da rede, altera o endereço de origem\
pra acessar serviço bloqueado - telegram - pode se usar vpn e ela eh utilizada como rota padrao. no proxy so da p usar http, vpn pode passar qlqr serviço\
proxy pode ser usado para monitorar usuários (utfpr p exemplo)\
vpn o pacote original ta dentro, encapsulado, do pacote novo gerado

## Sondagens
chava simetrica +-= chave unica\
tecnica fundamental eh o tunelamento\
em vpn o termo virtual existe pois essa tecnica depende de uma conexao temporaria, dessa forma utiliza-se o conceito de tunelamento p enviar pacotes de redes privadas por meio de redes publicas



# IDS


## IDS - Intrusion Detection System
- monitora o sistema, se ocorrer alguma anormalidade de segurança, reporta.
- só detecta, é detectivo
- problema: n toma atitudes \
IDSs baseados em redes podem apresentar problemas em ambientes de rede que utilizam switches ou apresentam grande parte do seu fluxo de pacotes criptografado.


## IPS 
- é um tipo de IDS, toma alguma atitude
- comum chamar tudo de IDS
- problema: falso positivo bloqueia coisa q n deveria

## IDPS
- IDS e IPS juntos

## HIDS - Host-based intrusion detection system
- sistema de detectção de intrusão baseado em hosts
- software
- monitora máquina
- MONITORA logs, processos, sistema de arquivos
- verifica localmente na máquina
- deve ser instalado em cada máquina, por isso geralmente é instalado em servidores, roteador padrão
- VANTAGENS:   
  - n tem problema cm switchs e criptografia
  - Pode detectar processos ou usuários maliciosos
- DESVANTAGENS:
  - instaçacao maquina p maquina
- exemplos
  - OSSEC
  - AIDE

## NIDS
- sistema de detecção de intrusão baseado em rede
- pode ser instalado em uma única máquina para monitorar a rede toda
- tem que receber informações de todos hosts, então só funciona em switchs que tem funcionalidade de espelhar portas
- mais utilizado para monitorar infos que vão para internet, e não internamente à rede
- MONITORA pacotes de rede
- máquina do NIDS não precisa ter IP, logo se não tiver IP não pode ser atacada via rede, mas é ruim para o admnistrador da rede
  - melhor seria alocar um IP fora da faixa da rede
  - ou criar VLAN somente para o NIDS
- não instala NIDS em máquinas que executem outros serviços
- VANTAGENS:
  - Ajuda na segurança de vários hosts da rede;
  - Pode ser invisível na rede
  - Não interfere nos fluxos da rede  
- DESVANTAGENS: 
  - n lida bem com switchs e criptografia, não vai analisar
- exemplos
  - Snort
  - Suricata

infos de HIDS e NIDS podem ser guardadas em outra maquina para melhorar a segurança (se ocorrer ataque, menos chance de perder dados)

*prova*
IDS baseado em assinaturas
- Vantagem: facil de ser desenvolvida
- Desvantagem: pode ser facil de burlar
- procura em trafego de rede de bytes ou seqüências de pacotes conhecidos como maliciosos. 
- vírus novo não está na base de assinaturas, então passa pelo IDS sem alerta (falso negativo)

sondagem - \
Uma assinatura é composta por uma seqüência de bytes que representam um ataque. Quando é encontrado no trafego da rede algum código que seja idêntico às assinaturas, é uma provável indicação de ataque. Os SDI utilizam esta abordagem para a detecção de intrusão, através da utilização de expressões regulares, análise de contexto ou linguagens de assinatura, os pacotes de rede são analisados e comparados com uma base de dados de assinaturas. Um exemplo de assinatura seria a string /etc/shadow na qual, qualquer pacote de rede utilizando por exemplo, Telnet, que apresente um conjunto de caracteres similares à este, irá gerar um alerta, como por exemplo com o comando: cat /etc/shadow

*prova*
IDS baseado em comportamento/anomalia
- exemplo: analise de acesso de funcionarios
  - constroi sua base de dados de horarios que um funcionario geralmente loga no sistema, se algum dia houver um login em horario muito diferente, vai gerar um alerta.
- melhor p encontrar ataques novos, pois tudo que será novo, será considerado uma anomalia
- gera mais falsos positivos

sondagem - 
- Mais complicado de configurar em relação ao baseado à assinatura
- As anomalias são consideradas ataques
- Pode produzir mais falsos positivos do que o baseado em assinatura
- Capaz de identificar ataques novos ou desconhecidos

Falso positivo
- IDS fica gerando alertas de coisas que na verdade não estão ocorrendo
- pode acontecer de dar positivo verdadeiro, e o adm ignorar
- pode ofuscar uma mensagem realmente importante no meio dos falsos positivos

Falso negativo
- Ocorre problema de segurança e IDS não alerta
- mais severo que o anterior


OSSEC pode ser usado em qlqr servidor
Snort tem q estar em uma maquina isolada



- identificar e reagir contra possíveis problemas de segurança
IPS
IDPS




# Firewall

diferença para o switch:\
firewall filtra rapidamente tudo que vem na rede e bloqueia ou libera, se algo é preciso ser
analisado mais a fundo, como analisar um detalhe de um pacote, deve-se utilizar switch


isola a rede de um ambiente hostil (internet).

composto por regras que ditam o que entra e sai e políticas q eh implantada por meio de regras

não impede de pegar virus


controla o q entra e sai da rede

2 tipos de politica
- liberar tudo\
tudo que não está bloqueado é liberado\
cria regra de bloqueios


- bloquear tudo\
bloqueia tudo que não é liberado\
tende a ser mais segura\
cria regra de liberar

## Projetos de firewall:
- host screened - host filtrado\
não pode ser acessado como servidor

- host bastion - host bastião\
pode ser acessado como servidor\
so deve ser acessado para serviços q propoe, como BD

- demilitarized zone - DMZ - zona desmilitarizada
LAN bastião\
controla por firewall qm pode acessar as maquinas na rede

- Hosts e firewalls invisiveis\
ips estão se esgotando, ficando caro, então tem duas soluções pra isso:
  - Filtragem bridge:\
    utiliza camada de enlace, filtra o que passa de um segmento a outro e eh invisivel, ja que n precisa de um ip e 
    diminui a chance de ser invadido.
    
  - NAT:
    esconde os endereços das máquinas da rede local atrás de um único endereço do roteador para ser roteado na internet


- proxy – Muitos Firewalls fazer o serviço de proxy e podem fazer pedidos de conexão em nomes de outros hosts;

- Gerador de logs – Em termos de segurança, quanto mais informações sobre sua rede e Firewall melhor. Então a
                    grande maioria dos Firewalls possuem mecanismos de log, que registram desde um pacote passando
                    pela rede, até atividades anormais, é claro que tudo configurável (o administrador escolhe o 
                    que vai registrar ou não);
                    
- Balanceamento de carga, Qualidade de Serviço (QoS) e Tolerância a Falhas: Alguns Firewalls conseguem priorizar 
                    serviços de redes, fazer balanceamento de carga de dados serviços de redes, ou mesmo tomar 
                    alguma atitude em caso de falhas de serviços de redes;
                   
- IDS: Alguns Firewalls possuem capacidade de interagir com Sistemas de Dectecção de Intrusão de redes ou de hosts.
                    A lista de funcionalidades poderia ser enorme, tanto é que muita gente hoje não sabe mais qual 
                    é a função básica de um Firewall, de tantas funcionalidades que este agregou ao longo do tempo;
                    
Mas uma coisa é certa o uso de Firewalls é indispensável para qualquer rede de computadores.





# iptables




