# Firewall
diferença para o switch:
firewall filtra rapidamente tudo que vem na rede e bloqueia ou libera, se algo é preciso ser
analisado mais a fundo, como analisar um detalhe de um pacote, deve-se utilizar switch\
isola a rede de um ambiente hostil (internet).\
composto por regras que ditam o que entra e sai e políticas q eh implantada por meio de regras\
não impede de pegar virus\

2 tipos de politica
- liberar tudo\
tudo que não está bloqueado é liberado\
cria regra de bloqueios


- bloquear tudo
bloqueia tudo que não é liberado\
tende a ser mais segura\
cria regra de liberar

Projetos de firewall:\
- host screened - host filtrado\
não pode ser acessado como servidor

- host bastion - host bastião\
pode ser acessado como servidor

- demilitarized zone - DMZ - zona deslimitarizada
?

- bridge 
?


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







