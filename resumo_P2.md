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



# IDS





# Firewall





# iptables




