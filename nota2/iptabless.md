# TABLES



**PROVA**:\
TRADUÇÃO DE REGRAS


para validar a regra, também é necessário fazer o caminho de volta do pacote


## FILTER 
nao precisa da opção -t 

### situações
vêm com politica padrão (accept)

* input
  * firewall recebe o pacote como entrada
  * o ip de destino do pacote é o firewall 

* output
  * firewall manda o pacote para outra maquina
  * o ip de origem é o firewall

* foward
  * pacote só passa pelo firewall
  * nem o ip de origem nem o de destino é o firewall 

não especifica porta do lado do cliente (porta de origem é alta e aleatória)

## nat


## MANGLE




## Regras 

![image](https://user-images.githubusercontent.com/37521313/207440324-9153995f-187d-47d8-9580-509ecd6f4021.png)

