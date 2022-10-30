# Análise prática de segurança

**Autor:** Alexandre Aparecido Scrocaro Junior \
**email:** alescrocaro@gmail.com

**Professor:** Luiz Arthur Feitosa dos Santos\
**Universidade Tecnológica Federal do Paraná (UTFPR)**

[link para a especificação do trabalho](https://moodle.utfpr.edu.br/mod/assign/view.php?id=1322162)

## Usuários não autorizados ou suspeitos

Primeiramente, fiz a conexão com a máquina via ssh, e então utilizei o comando w para verificar se havia mais algum usuário conectado a máquina. Como pode ser visto abaixo, apenas a minha instância estava sendo processada.\
![comando w](https://user-images.githubusercontent.com/37521313/198883005-5544bea9-80a9-4d05-8107-0ef5ad501851.png)

Então utilizei o comando last para visualizar as últimas ações de logon, tentando visualizar usuários não autorizados. Como visto abaixo, há um usuário proxy e outro usuário reboot que são suspeitos.\
![comando last](https://user-images.githubusercontent.com/37521313/198883560-9a4c2ae5-46b1-4b0e-ae01-7895c04caea7.png)

Ao utilizar o comando "cat ~/etc/passwd" consigo visualizar todos os usuários do sistema. Assim é possível visualizar que além do usuário root, o usuário uucp possui o UID = 0, sendo uma duplicata do root, isso é uma possível ameaça que deve ser verificada.\
![image](https://user-images.githubusercontent.com/37521313/198884549-5dbfec63-d648-46d2-a9f1-34aaa22e9988.png)


Agora, utilizei o comando "cat ~/etc/shadow", para visualizar o arquivo de senhas. Como pode ser visto abaixo, há usuários estranhos, como o "nobody" e "proxy" que devem ser verificados.\
![arquivo de senhas shadow](https://user-images.githubusercontent.com/37521313/198884214-f0fcf05e-9d09-415a-86fa-af738be8b681.png)

## Processos suspeitos e/ou maliciosos



