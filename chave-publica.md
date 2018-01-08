# Configurar conjunto de chaves para conexão direta nos servidores Linux

### Criação da chave

Navegue até a home do seu usuário e acesse a pasta `.ssh`
```sh
$ cd ~/.ssh
```
Caso a pasta não exista, execute o comando abaixo para criá-la
```sh
$ sudo mkdir -p ~/.ssh/
```
Crie sua chave pública executando o comando
```sh
$ sudo ssh-keygen -f id_rsa
```
Será solicitado a senha para sua chave, deixe em branco para conexão direta ou digite uma senha. Caso use uma senha, todas as vezes que tentar acessar o servidor remoto com sua chave, esta senha será solicitada.

Conceda permissão para leitura/execução da chave gerada
```sh
$ sudo chmod +rx id_rsa
```

### Autorização no servidor

Para conexão direta com o servidor, você deverá acessar o servidor destino e navegar até a pasta do usuário que você irá autorizar a chave pública, por exemplo:

Você quer autorizar a conexão com chave pública, no servidor de testes da CRA para o usuário `cra`, então acesse o servidor
```sh
$ ssh cra@crateste.com.br
```
Digite a senha para se conectar normalmente.

Navegue até a pasta do usuário e altere o arquivo `.ssh/authorized_keys`
```sh
$ cd ~/.ssh/
sudo vim authorized_keys
```
Após abrir o arquivo para edição, pressione a tecla `i` para entrar no modo insert do vim e cole o conteúdo do arquivo `id_rsa.pub` gerado anteriormente.
Aperte `ESC` para sair do mnodo insert e digite o comando `:x` e pressione enter. O arquivo será fechado e salvo.

Desconecte-se do servidor e tente novamente, a conexão deverá ser realizada sem a utilização da senha. Caso você tenha gerado sua chave pública utilizando uma senha, esta senha deverá ser informada todas as vezes que você realizar a conexão.
