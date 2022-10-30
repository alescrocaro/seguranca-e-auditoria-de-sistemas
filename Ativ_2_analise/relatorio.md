# Análise prática de segurança

**Autor:** Alexandre Aparecido Scrocaro Junior \
**email:** alescrocaro@gmail.com

**Professor:** Luiz Arthur Feitosa dos Santos\
**Universidade Tecnológica Federal do Paraná (UTFPR)**

[link para a especificação do trabalho](https://moodle.utfpr.edu.br/mod/assign/view.php?id=1322162)

## Introdução a respeito dos procedimentos realizados
TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO 







## Descrição dos passos realizados Tal descrição deve apresentar comandos utilizados, resultados obtidos e conclusão parcial de cada resultado

### Usuários não autorizados ou suspeitos

Primeiramente, fiz a conexão com a máquina via ssh, e então utilizei o comando w para verificar se havia mais algum usuário conectado a máquina. Como pode ser visto abaixo, apenas a minha instância estava sendo processada.\
![w](https://user-images.githubusercontent.com/37521313/198883005-5544bea9-80a9-4d05-8107-0ef5ad501851.png)

Então utilizei o comando last para visualizar as últimas ações de logon, tentando visualizar usuários não autorizados. Como visto abaixo, há um usuário proxy e outro usuário reboot que são suspeitos.\
![last](https://user-images.githubusercontent.com/37521313/198883560-9a4c2ae5-46b1-4b0e-ae01-7895c04caea7.png)

Ao utilizar o comando "cat ~/etc/passwd" consigo visualizar todos os usuários do sistema. Assim é possível visualizar que além do usuário root, o usuário uucp possui o UID = 0, sendo uma duplicata do root, isso é uma possível ameaça que deve ser verificada.\
![cat etc passwd](https://user-images.githubusercontent.com/37521313/198884549-5dbfec63-d648-46d2-a9f1-34aaa22e9988.png)


Agora, utilizei o comando "cat ~/etc/shadow", para visualizar o arquivo de senhas. Como pode ser visto abaixo, há usuários estranhos, como o "nobody" e "proxy" que devem ser verificados.\
![arquivo de senhas shadow](https://user-images.githubusercontent.com/37521313/198884214-f0fcf05e-9d09-415a-86fa-af738be8b681.png)



### Processos suspeitos e/ou maliciosos
Tais processos podem servir para o atacante explorar uma falha na máquina e devem ser fechados, outra forma de recuperar o sistema contra tais processos é reinstalar uma versão mais atualizada do mesmo.\

Para visualizar todos processos em execução na máquina (de todos usuários, devido a opção 'a') utilizei o comando "ps aux", além do "pstree" para relacionar os processos. Como pode ser observado abaixo, há processos que provavelmente não deveriam estar em execução, como o caso do mysql e do nfs, é necessário, no mínimo, matar esses processos.\
![ps aux](https://user-images.githubusercontent.com/37521313/198886506-733a48b8-6ce4-4c6f-88c9-e67f76f0d7d1.png)

![pstree](https://user-images.githubusercontent.com/37521313/198886654-27e678e5-e4ca-4b0e-855d-c086f3520936.png)

Além disso, é possível observar os processos visualizando kernel diretamente com o comando "cat /proc/\*/stat | awk '{print $1, $2}'". Dessa forma podemos visualizar processos que possivelmente foram escondidos por um invasor. Com isso descobri o processo rpc.mountd, que é um risco à segurança e pode ser usado (ou ter sido usado) por um invasor.\
![processos vistos diretamente no kernel](https://user-images.githubusercontent.com/37521313/198887345-1efd9953-c747-4591-a70e-6b051f06b30f.png)

Para matar um processo (utilizarei o mysql como exemplo), utilizei o comando "kill -811 pid". Ao utilizar o comando "ps aux" novamente pode ser observado que tal comando sumiu.

# Alterações ou possíveis alterações no sistema de arquivos

Para buscar por alterações, fiz a instalação do rpm, que fará tal verificação. Para tanto, utilizei o comando "rpm -Va > /tmp/rpmVA.log"; entretanto nenhuma saída foi gerada, então imagino que esteja tudo correto.

# Análise nos arquivos de log do sistema que podem apontar atividades maliciosas ou suspeitas

Os arquivos de log são locais onde se pode obter informações preciosas à respeito da segurança da máquina, então deve-se realizar consultas neles periodicamente.

Utilizei o comando "grep fail auth.log" e "grep repeat auth.log"; o segundo não retornou nada, já o primeiro retorno as duas mensagens vistas abaixo que não aparentam representar perigos à segurança.\
![grep fail auth.log](https://user-images.githubusercontent.com/37521313/198889337-484deb72-d843-49bb-8de0-ae4e8865608b.png)

Além disso, utilizei os comandos "zgrep fail auth.log*" e "zgrep repeat auth.log*". Como mostrado nas capturas abaixo.
![zgrep fail auth.log*](https://user-images.githubusercontent.com/37521313/198889518-edabec55-4ecc-4181-8d6f-2fce3b13129c.png)
![zgrep repeat auth.log*](https://user-images.githubusercontent.com/37521313/198889550-64a7e744-d37f-40ae-9252-6dca75bcdaaa.png)

Analizando as capturas acima, percebe-se que há algo estranho no arquivo 'auth.log.4.gz', com várias falhas de autenticação seguidas, isso pode ser um problema, então iremos utilizar o comando "zcat auth.log.4.gz" para analisar.\
A saída desse comando não gerou nenhuma ameaça aparente acerca do que eu estava procurando, porém encontrei outra ameaça (que pode ser vista no printscreen abaixo). Essa adição do usuário 'dacom' aos grupos é suspeita e deve ser analisada, principalmente por ele ter sido adicionado ao grupo 'adm'.\
![zcat auth.log.4.gz](https://user-images.githubusercontent.com/37521313/198889828-3a9e2b78-19b5-4ce0-9786-250d5428fbfb.png)

Para verificar últimas tentativas de logon, utilizei o comando "tail -f auth.log" (no diretorio /var/log), e analisando a saída, vista abaixo, há indícios de que está sendo executado um script (devido à várias e repetidas sessões criadas e fechadas). \
![tail -f auth.log](https://user-images.githubusercontent.com/37521313/198890633-d8fc0e1f-47e1-49b5-bbeb-5e73d52d2523.png)

Fiz uma breve análise e pesquisas do que isso poderia ser, mas não encontrei muitos resultados.\
![analise cron](https://user-images.githubusercontent.com/37521313/198890764-28dcca5c-0ee8-45bb-948a-4013ced7ef70.png)




## Análise/resumo geral a respeito do resultado obtido na análise realizada, tentando correlacionar os dados obtidos em cada um dos passos da prática de segurança. Se foram encontrados problemas, aponte esses problemas, comente como esses podem afetar ou já afetaram a segurança do sistema e se você conseguir apresente possíveis soluções
TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO 

## Conclusão a respeito dos passos realizados e de possíveis facilidades/dificuldades encontradas durante a realização desses passos.
TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO 

## Comparar PenTeste com as Práticas de segurança, principalmente em relação aos resultados obtidos.
TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO 

