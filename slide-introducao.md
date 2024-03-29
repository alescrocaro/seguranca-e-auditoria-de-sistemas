# elementos basicos da seguranca da informacao

## Confidencialidade
### O que é?
- informações só ficam disponíveis para quem tem permissão
    
### Como fornecer?
- **criptografia**
- controle de acesso de usuario

## Disponibilidade
### O que é?
- informação deve ficar disponível ao ser requisitada

### Como fornecer?
- redundancia
  -   backup
  -   internet de empresas diferentes
  -   no break
  -   RAID\
ao subir dados na nuvem, a confidencialidade pode diminuir (exemplo do dropbox e o responsavel pelo servidor (do dropbox) talvez pode ter acesso a informações do servidor (lado humano - o responsavel pode n ser de boa indole))

## Integridade
### O que é?
- informações não podem se corromper
- Não basta ter a informação ela precisa ser exata e correta
### Como fornecer?
- hash
  - algoritmo onde dada uma entrada de dados, é feito um calculo sobre e gera um unica saida (para dados diferentes, são geradas saídas diferentes)
  - não é criptografia, em hash não tem como voltar a saída para seu estado original - ele gera uma sequencia de caracteres para comparar as saidas

## Um elemento de segurança pode infuenciar outro
- Prover muita segurança em um elemento da informação pode gerar
insegurança a outro elemento.
- Exemplo,
caso apliquemos um alto grau de confidencialidade (uma chave criptográfca muito grande, ou várias fechaduras) podemos tornar a informação indisponível.\
Isto pode ocorrer, por exemplo, por que perdemos a chave criptográfca ou a chave da porta onde está a informação. Ou seja, a confidencialidade infuenciou na disponibilidade do exemplo anterior. Assim devemos ter cuidado e dosar as medidas de segurança. 
- Sempre avalie o custo e benefício/malefício de cada medida de segurança que você adotar

# outros elementos para manter a segurança de computadores
## Autenticidade:
Impedir que pessoas não autorizadas tenham acesso aos recursos computacionais, ou seja, é necessário a identifcação dos elementos que compõem uma transação eletrônica;
## Não-repúdio: 
Impedir a falsa negação de ações que alguém tenha realizado. O não repúdio pode ser entendido como sendo os esforços aplicados para garantir a autoria de determinadas ações;\
visa garantir que o autor não negue ter criado e assinado o documento\
exemplo de caixas eletronicos do banco com camera de segurança
## Auditoria: 
É a identifcação de ações/eventos ocorridos no sistema. A auditoria é feita através de análise de registros que identifquem:
- Ações realizadas; 
- Pessoas envolvidas;
- Ativos utilizados; 
- Operações realizadas; 
- Horários dos eventos/ações;  
- E qualquer dado relevante para realizar a auditoria.

# tipos de medidas de seguranca
antivirus encontra-se no mínimo nos 2 primeiros

## preventiva
firewall\
São medidas aplicadas para evitar/prevenir a ocorrência de problemas de segurança. Normalmente só é possível a prevenção de ataques conhecidos

## detectiva
IDS\
Medidas utilizadas para monitorar, identifcar, detectar e em alguns casos tomar alguma atitude/ação, frente a problemas de segurança que estão acontecendo

## corretiva
Backup\
Essa medidas tem como objetivo permitir a continuidade das operações do sistema. A medida corretiva é utilizada quando tudo mais falhou, ou seja, caso as medidas preventivas e detectivas não tenham sucesso, resta então aplicar medidas que corrijam os problemas que já ocorreram

# Hacker
- Originalmente o termo Hacker, designava qualquer pessoa extremamente especializada em uma determinada área.
- Cracker: Possui tanto conhecimento quanto um Hacker, mas com a diferença de que, para eles, não basta invadir sistemas, quebrar senhas, e descobrir falhas eles tem que fazer o mau. Cracker é o verdadeiro Hacker do mau.
- Atenção! Se um Hacker quiser realmente te invadir é bem provável que ele consiga, independente do nível de segurança que você empregue. Nós não vamos nos proteger deste tipo de invasor, mas sim dos que virão a seguir. Contra os Hackers podemos usar a técnica da avestruz, ou seja, enfia a cabeça na terra e se esconde! Utilizar muitas medidas de segurança podem chamar mais ainda a atenção do Hacker e agravar o problema.Se você estiver frustrado com a técnica da avestruz, pare e pense! Por que os bancos, mesmo com todo o investimento em segurança, ainda são roubados?
- Guru: O supra sumo dos Hackers. Hoje os sistemas são tão complexos que devem existir poucas pessoas com este título. Mas eles existem e são verdadeiros gênios.
## Classificando os hackers
- White hats (do bem): São os mocinhos, ou seja, os haceers que usam suas habilidades para propósitos legais, tal como, defender pessoas de ciberataques. Esse tipo de haceer normalmente é representado por profssionais da área de cibersegurança;
- Black hats (do mau): São os vilões, ou seja, são craceers que usam sua inteligência para fns maliciosos. Esses, invadem sistemas e normalmente destroem dados vitais e/ou interferem em serviços;
- Grey hats: (Faz coisas duvidosas, como invadir a empresa e alterar o BD, depois mostrar para a empresa. a empresa não pediu para fazer isso, vc cometeu um crime!) São haceers que podem trabalhar de forma ofensiva ou defensiva, dependendo da situação. Os Grey hats são a linha divisória entre os haceers e os craceers. Essa classifcação existe pois algumas pessoas são tanto Blace hats quanto White hats. Por fm, esse é um tipo difícil de se categorizar, pois não são bons nem maus. Um exemplo são haceers que querem testar alguma técnica de invasão, mas não pedem autorização para testá-la em uma empresa.

## Classificando os não hackers
- Lammers: Aquele que deseja aprender sobre haceers, e sai perguntando para todo mundo: “como eu me torno um haceer? O que devo fazer?”i. Os haceers, não gostam disso, e passam a chamar-lhes de Newbie (novatos).
- Wannabe: É um principiante que aprendeu a usar alguns programas, já prontos, para descobrir senhas ou invadir sistemas. Os Wannabes ainda não tem capacidade de criar suas próprias técnicas.
- Larva: Este já está quase se tornando um Hacker. Este já consegue desenvolver suas próprias técnicas de como invadir sistemas.


Arackers: São os Hackers de Araque, são a maioria absoluta no submundo cibernético. Algo em torno de 99,9%
tentando invadir sistemas ele trás vulnerabilidades para dentro de seu próprio sistema e o pior, sempre temos um Aracker dentro de nosso ambiente de trabalho ou em casa.


## O que os hackers exploram?
- Sistemas Operacionais:\
Muitos administradores instalam sistemas operacionais e não os confguram, ou seja, deixam com configuração padrão, o que normalmente resulta em brechas que podem ser exploradas durante ciberataques;

- Aplicações:\
Softwares normalmente não são testados contra vulnerabilidades de segurança durante o seu desenvolvimento, o que pode acarretar em falhas que podem ser exploradas;

- Shrink-wrap code:\
Muitos softwares de prateleira vêm com características extras que o usuário final não conhece e essas podem ser usadas por haceers. Um exemplo é o Microsoft Word que permite que haceers executem programas através de macros;

- Má configuração:\
Sistemas também podem ser configurados erroneamente ou deixados com baixo nível de segurança, para facilitar seu uso. Contudo isso resulta em vulnerabilidades que podem ser exploradas durante ataques

## Fases/passos de hacking

1. Reconhecendo\
    pesquisas: recolhe infos na internet sobre a instituição/pessoa\
    passivo:\ 
    obter infos sem que o alvo tome conhecimento. Exemplo: observar o habito de funcionários em uma empresa alvo
    
    
    ativo:\
    sondar infos para descobrir redes, hosts, IPs e serviços. Aumenta as chances do ataque ser identificado.\
\
    fase mais superfcial.
    
    
2.  Escaneamento
    Fazer uma análise mais profunda do alvo utilizando as informações obtidas na fase anterior\
    mais técnica que a anterior\

    fase consiste em uma análise mais profunda e detalhada das tecnologias e vulnerabilidades da vítima.\
    
    Ferramentas:
    - Discadores (dialers);
    - Escâneres de portas;
    - Mapeamento de rede (descobrir maquinas que existem na rede);
    - Varredores (sweepers);
    - Escâneres de vulnerabilidades.

\
    Procura de qualquer info que possa ajudar a realizar o ataque (como nomes, computadores, ips, contas de usuarios)\
Por exemplo, a fase de reconhecimento pode ter mostrado que a rede alvo tem 500 computadores conectados em uma subrede dentro de um prédio. Já a presente fase pode trazer informações que algumas dessas máquinas possuem o sistema operacional Windows e que outras executam FTP.\

passivo: não tem interação, só observa\
ativo: tem interação, 'testa se a porta (da casa) ta aberta'\


3. Ganhando acesso: 
é onde a mágica acontece. Pois, é a fase na qual realmente o hacker invade a vítima. Para ganhar acesso o haceer utiliza as informações obtidas nas fases anteriores.\
Os métodos de invasão podem ser:
- Via Internet - WAN;
- Rede local – LAN;
- Localmente no computador;
- offline

invasões offline/localmente no computador são as mais devastadoras


4. Mantendo acesso
provável que o hacker queira manter o acesso para realizar ações futuras\
A manutenção do acesso é normalmente realizada através de backdoors, rootkits e trojans\
Alguns hackers chegam ao ponto de melhorar o nível de segurança da máquina invadida para ter exclusividade (evitar outros haceers).


5. Cobrindo os rastros
Com a máquina já comprometida, o último passo é apagar todos os indícios que denunciem a invasão. Isso também impede alguma ação legal por parte da vítima. Apagar as pistas de uma ciber invasão signifca:
- Remover dados em arquivos de logs;
- Apagar alertas de sistemas de detecção de intrusão
- Ocultar arquivos.

Outro exemplo é quando o hacker utiliza túneis criptográficos para impedir que um possível sistema de segurança compreenda a ação do haceer (comandos, arquivos, etc).


## Hacktivismo
Hoje, a ideia de grupos hackers é maior do que a de um individuo sozinho. (Anonymous)\

Alvos dos hackers:
- sites famosos
- empresas de tecnologia
- empresas de segurança
- concorrentes
- governo
- vitimas aleatórias


## Ataques a pessoas comuns
Os Hackers de verdade difcilmente vão querer invadir o computador de uma pessoa comum. Isto por que na verdade um ataque pode ser tedioso e caso o Hacker não tenha uma motivação ele não vai fazer o ataque só por fazer! Mas isto não se aplica aos não Hackers que atacam só por diversão. Então, ataques a pessoas comuns geralmente são ataques de:

- Ataques a Privacidade: É o ataque mais comum ao usuário domestico. Já que como é da natureza humana, os atacantes tem compulsão em dar uma olhadinha na vida da vitima e nos dias atuais os computadores são pratos cheios para este propósito.
- Destruição: Este tipo de ação pode ser considerada a mais destrutiva, pois pode destruir informações segundos, esses ataques podem ocorrer devido a vírus (o mais comum) e Craceers. O pior nestes casos é que usuários domésticos não têm o costume de fazer copias de segurança.
- Obtenção de Vantagens: Para obter vantagens causando incidentes de segurança nos computadores pessoais, geralmente é necessário a utilização de técnicas no qual primeiro a vitima será exposta a ataques de privacidade ou destruição. As motivações deste tipo de ataque são tão distintas quanto seu próprio objetivo real.


## Um pouco mais a respeito de ciberataques

- passivos
    - rouba os dados. tentam obter informações a respeito do sistema/rede, ou seja, não altera o estado da vítima. Assim, ataques passivos afetem contra a confdencialidade.
- ativos
    - rouba os dados e destroi outros. alteram o sistema ou rede que está sob ataque.

# Vírus
software cujo objetivo principal não é fazer maldade, mas reproduzir, até q em algum momento ele faz algo ruim.\
Hoje em dia o vírus é discreto, para conseguir se proliferar mais/roubar dados\
Mitigar: o virus pode ser amenizado, mas dificilmente 100% erradicado\

WORM: não precisa ser iniciado, se prolifera sozinho\

RANSOMWARE: qualquer virus/malware de sequestro de dados, feito por meio de criptografia, que usa como refém arquivos pessoais da própria vítima e cobra resgate para restabelecer o acesso a estes arquivos. \

SPYWARE: Fica observando\

TROJAN: Um aplicativo com um malware oculto\

Se previnir de virus: manter softwares atualizados

# DoS
ataque local, torna um serviço lento ou indisponivel\
ataque vem de uma só fonte\
virus antigamente usava ideia de DoS, Exemplo: SO\
um ataque vindo de varias maquinas pode ser um DoS\
ping da morte: gerar muitos pings para uma determinada máquina\
muito complicado de ser resolvido:\
pode ser resolvido com DoS (bloquear faixa de ips, usar captcha para verificar se eh humano se n for bloqueia, tenta ver o padrão pra bloquear)\

como se prooteger:\
    manter sistema atualizado, para evitar vulnerabilidades\
    retira serviços necessários da rede

# DDoS
Ataque vem de mais de uma fonte, via rede.\
pode não ser um ataque massivo, da pra realizar ataques com 1, 2 ou 5 pacotes\
um ataque vindo de apenas uma maquina não pode ser um DDoS\


# Engenharia social
é um método não técnico de quebrar a segurança de sistemas ou redes. É o processo de enganar usuários de sistemas/redes e convencê-los de fornecer informações que podem ser usadas para anular ou burlar sistemas de segurança e/ou obter informações sensíveis.\
arte de persuadir alguem para fazer o q vc quer\
golpe de telefone sequestro\
fake news tb se encaixa aqui\
***combatido com treinamento das pessoas***\

Baseada em humanos: refere-se à interação pessoa-a-pessoa para conseguir as informações desejadas. Um exemplo é ligar para a empresa e tentar conseguir senhas;

Baseada em computadores: nessa o haceer utiliza algum meio computacional para tentar obter informações sensíveis. Um exemplo é enviar um e-mail para a vítima pedindo que a vítima entre com seu usuário e senha em uma página Web falsa (phishing).


# Criptografia
embaralha informação e a torna incompreensível\
ideia antiga\
antigamente o segredo da criptografia era o algoritmo que criptografava\
ou seja, depende do método usado para criptografar, esse não pode ser o segredo da criptografia, pois basta tê-lo para conseguir descriptografar\
agora o algoritmo de criptografia é publico, atualmente há a ideia de chaves (binárias)\
    chave geralmente é um conjunto de bits\
A chave consiste em uma string que pode ser alterada sempre que necessário.\
A força da chave geralmente se dá pela quantidade de bits que a compõem\

2 tipos:\
única: a mesma chave criptografa e descriptografa a informação. *Não é bom para compartilhar infos com outras pessoas*.  *Todavia é mais rápido, utilizado para criptografar coisas privadas, como HD pessoal.*\
pública e privada: tem a chave privada e a pública, a privada é pessoal e usada para **descriptografar** e a pública pode ser compartilhada e é usada para **criptografar**. ambas chaves estão 'conectadas'\
O custo de descriptografar usando chave privada é maior do q usando chave unica\

processo de assinatura online (certificado digital) é ao contrário: privada criptografa e publica descriptografa.\ 

Não impede que dados sejam alterados e apagados\




##### elementos de segurança referenciados em TCP/IP\

Fisica:\
inseguro: radio frequencia (wireless)\
mais seguro: fibra (mais viável. o cabo pressurizado é mais seguro, porém não é muito utilizado pela população em geral)\


Enlace:\
mais seguro: cabo? wpa2, switch (substitui o hub - que era utilizado antigamente para roubar senhas), vpn\


Inter-rede:\
mais seguro: IPSec (melhoria no protocolo ip por questões de segurança, mas não é padrão); roteador (só faz filtragens de origem, destino e protocolo)\

Transporte:\
mais seguro: firewall (surgiu para melhorar a segurança que o roteador provinha)\

Aplicação:\
mais seguro: ssh, openVPN, https, proxy (filtragem de conteúdo)\


***NADA É TOTALMENTE SEGURO!!!***
























