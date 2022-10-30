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

Além disso, é possível observar os processos visualizando kernel diretamente com o comando "cat /proc/\*/stat | awk '{print $1, $2}'". Dessa forma podemos visualizar processos que possivelmente foram escondidos por um invasor.\
![processos vistos diretamente no kernel](https://user-images.githubusercontent.com/37521313/198887154-fca8e89d-0d83-40a3-8909-bef369cffe15.png)


Para matar um processo (utilizarei o mysql como exemplo), utilizei o comando "kill -811 pid". Ao utilizar o comando "ps aux" novamente pode ser observado que tal comando sumiu.






## Análise/resumo geral a respeito do resultado obtido na análise realizada, tentando correlacionar os dados obtidos em cada um dos passos da prática de segurança. Se foram encontrados problemas, aponte esses problemas, comente como esses podem afetar ou já afetaram a segurança do sistema e se você conseguir apresente possíveis soluções
TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO 

## Conclusão a respeito dos passos realizados e de possíveis facilidades/dificuldades encontradas durante a realização desses passos.
TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO 

## Comparar PenTeste com as Práticas de segurança, principalmente em relação aos resultados obtidos.
TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO TODO 

