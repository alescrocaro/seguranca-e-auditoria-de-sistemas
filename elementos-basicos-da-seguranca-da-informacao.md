# Confidencialidade
## O que é?
- informações só ficam disponíveis para quem tem permissão
    
## Como fornecer?
- criptografia
   -  o mais simples é usuário com senha

# Disponibilidade
## O que é?
- ato de ficar disponível ao ser requisitado

## Como fornecer?
- redundancia
  -   backup
  -   internet de empresas diferentes
  -   no break
- ao subir dados na nuvem, a confidencialidade pode diminuir (exemplo do dropbox e o responsavel pelo servidor (do dropbox) talvez pode ter acesso a informações do servidor (lado humano - o responsavel pode n ser de boa indole))

# Integridade
## O que é?
- informações não podem se corromper
- Não basta ter a informação ela precisa ser exata e correta
## Como fornecer?
- hash
  - algoritmo onde dada uma entrada de dados, é feito um calculo sobre e gera um unica saida (para dados diferentes, são geradas saídas diferentes)
  - não é criptografia, em hash não tem como voltar a saída para seu estado original - ele gera uma sequencia de caracteres para comparar as saidas

