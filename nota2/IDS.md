IDS 
- monitora o sistema, se ocorrer alguma anormalidade de segurança, reporta.
- só detecta, é detectivo
- problema: n toma atitudes

IPS 
- é um tipo de IDS, toma alguma atitude
- comum chamar tudo de IDS
- problema: falso positivo bloqueia cois aq n deveria

IDPS
- IDS e IPS juntos

HIDS
- sistema de detectção de intrusão baseado em hosts
- software
- monitora máquina
- verifica logs, processos, sistema de arquivos
- verifica localmente na máquina
- deve ser instalado em cada máquina, por isso geralmente é instalado em servidores, roteador padrão
- desvantagem: instaçacao maquina p maquina
- vantagem: n tem problema cm switchs e criptografia

NIDS
- sistema de detecção de intrusão baseado em rede
- pode ser instalado em uma única máquina para monitorar a rede toda
- tem que receber informações de todos hosts, então só funciona em switchs que tem funcionalidade de espelhar portas
- mais utilizado para monitorar infos que vão para internet, e não internamente à rede
- problema: n lida bem com switchs e criptografia, não vai analisar
- analisa pacotes de rede
- máquina do NIDS não precisa ter IP, logo se não tiver IP não pode ser atacada via rede, mas é ruim para o admnistrador da rede
  - melhor seria alocar um IP fora da faixa da rede
  - ou criar VLAN somente para o NIDS
- não instala NIDS em máquinas que executem outros serviços

infos de HIDS e NIDS podem ser guardadas em outra maquina para melhorar a segurança (se ocorrer ataque, menos chance de perder dados)

*prova*
IDS baseado em assinaturas
- Vantagem: facil de ser desenvolvida
- Desvantagem: pode ser facil de burlar
- procura em trafego de rede de bytes ou seqüências de pacotes conhecidos como maliciosos. 
- vírus novo não está na base de assinaturas, então passa pelo IDS sem alerta (falso negativo)
- acontece mais falsos positivos

*prova*
IDS baseado em comportamento/anomalia
- exemplo: analise de acesso de funcionarios
  - constroi sua base dedados de horarios que um funcionario geralmente loga no sistema, se algum dia houver um login em horario muito diferente, vai gerar um alerta.
- melhor p encontrar ataques novos, pois tudo que será novo, será considerado uma anomalia
- gera mais falsos positivos

Falso positivo
- IDS fica gerando alertas de coisas que na verdade não estão ocorrendo
- pode acontecer de dar positivo verdadeiro, e o adm ignorar
- pode ofuscar uma mensagem realmente importante no meio dos falsos positivos

Falso negativo
- Ocorre problema de segurança e IDS não alerta
- mais severo que o anterior
- 





