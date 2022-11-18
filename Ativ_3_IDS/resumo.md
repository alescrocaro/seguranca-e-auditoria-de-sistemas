Nesta atividade você deve fazer uma pesquisa a respeito de IDS (Intrusion Detection Systems) 
e depois escrever um resumo manuscrito a respeito do assunto pesquisado. Tal resumo deve ter 
as seguintes estruturas/conteúdos:

1. Introdução
2. Definições/contextualização;
3. Tipos de IDS;
4. Uma ferramenta prática de IDS;
4. Conclusão (vantagens/desvantagens);
5. Bibliografia.

Observações:\
i) Tal resumo não deve ter mais do que três páginas.\
ii) Para a entrega desta atividade, o acadêmico deve enviar uma foto do texto manuscrito aqui 
nesta atividade do Moodle. Atenção, tirar uma foto legível e de boa qualidade para que o professor 
possa ler o texto, caso contrário o trabalho será desconsiderado.


# Introdução

IDS é a sigla de Intrusion Detection System, ou Sistema de Detecção de intrusão é por meio desse tipo 
de sistema que será possível identificar ações de atacantes (usuários não autorizados), e até funcionários
da empresa com más intenções.





# Definições/contextualização

Um IDS é um software que irá monitorar a rede com intuito de encontrar atividades maliciosas ou 
violações da política de uma empresa, por exemplo. Qualquer indício de uma dessas duas será reportado 
e, dependendo do tipo do IDS (os tipos serão abordados posteriormente), pode tomar alguma atitude em
frente à ameaça.\
Posteriormente também utilizarei os termos, muito utilizados nesse contexto, falso positivo e falso 
negativo. Em suma, o primeiro acontece ao emitir um alerta quando na verdade não há nenhuma ameaça,
já o segundo é quando uma há uma ameaça e nenhum alerta é emitido.





# Tipos de IDS

- IPS\
Comumente também é chamado de IDS, porém o IPS toma atitudes frente à ameaças.


- HIDS - Host-based intrusion detection systems\
É um sistema de detecção de intrusão baseado em hosts.\
Monitora o sistema de arquivos, arquivos de logs e processos.\
Deve ser instalado em cada máquina, por isso geralmente é instalado em servidores ou roteadores padrão.


- NIDS - Network intrusion detection systems\
Sistema de detecção de intrusão baseado em rede.\
Mais utilizado para monitorar informações que vão para internet, ou seja, que saem da rede local.\
Pode ser instalado em uma única máquina para monitorar a rede toda.\
Tem que receber informações de todos hosts, então só funciona em switchs que têm funcionalidade de 
espelhar portas.


- Baseado em comportamento/anomalias:\
Uma nova tecnologia que tem o objetivo de detectar e se adaptar para reconhecer ataques desconhecidos
Esse método utiliza conceitos de aprendizagem de máquina para criar um modelo de atividades conhecidas,
então tem uma base de dados de atividades normais do sistema acusando mais facilmente uma atividade
desconhecida como uma possível ameaça.


- Baseado em assinaturas:\ 
Essa tecnologia irá detectar possíveis ameaças utilizando assinaturas conhecidas para comparar com
os dados (sequência de bytes) que trafegam na rede. É semelhante aos antivirus, pois utiliza assinaturas
pré definidas para identificar ameaças.





# Uma ferramenta prática de IDS

- OSSEC\
Criada pelo brasileiro Daniel Cid, é uma ferramenta HIDS que, dentre outras propostas, analisa arquivos 
de log, verifica a integridade do sistema e detecta root kits.





# Conclusão (vantagens/desvantagens);

Cada tipo de IDS tem suas particularidades, então cada um dos tipos terá uma utilização diferente com 
suas próprias vantagens e desvantagens, como pode ser visto abaixo:

- IPS\
Vantagem: Toma atitude frente à ameaças\
Desvantagem: Dispara falsos positivos, bloqueando ações que não deveria.

- HIDS - Host-based intrusion detection systems\
Vantagem: Não tem problemas com switchs ou criptografia e pode detectar processos ou usuários 
          maliciosos\
Desvantagem: Instalação em cada máquina. 

- NIDS - Network intrusion detection systems\
Vantagem: Ajuda na segurança de vários hosts da rede, não interfere nos fluxos da rede e pode ser
          invisível na rede (utilizando uma faixa de ips fora da faixa da LAN, porém pode dificultar
          as ações do administrador da rede)\
Desvantagem: Não lida bem com switchs e criptografia.

- Baseado em comportamento/anomalias:\
Vantagem: Encontra novos ataques, pois tudo que é novo na rede é considerado uma anomalia\
Desvantagem: Dispara falsos positivos, pois nem tudo que é novo na rede é realmente uma anomalia.

- Baseado em assinaturas:\ 
Vantagem: Fácil de ser desenvolvida\
Desvantagem: Pode ser fácil de burlar, não detecta novos ataques





# Bibliografia

Além das informações que anotei nas aulas em [meu github](https://github.com/alescrocaro/seguranca-e-auditoria-de-sistemas), 
também consultei [esse](https://www.barracuda.com/glossary/intrusion-detection-system) site.

