# Instalando e configurando um servidor Redis no PHP

### Instale o servidor do Redis
```sh
$ apt-get install redis-server
```
Fedora
```sh
$ yum install redis -y  
```

### Instale a extensão do Redis para PHP

```sh
$ apt-get install php-redis
```

fedora 

```sh
yum install php56-pecl-redis
```

Defina uma senha para o servidor Redis

Para adicionar uma camada extra de segurança à sua instalação do Redis, é recomendável definir uma senha para acessar os dados do servidor. Editaremos o mesmo arquivo de configuração da etapa anterior,

```sh
vim /etc/redis/redis.conf
```

fedora 

```sh
vim /etc/redis.conf
```

Agora, remova o comentário da linha que contém requirepass e defina uma senha forte:

```
requirepass SUA_SENHA
```

Reinicie o serviço Redis para que as alterações entrem em vigor:

``` sh
service redis-server restart
```

Testar conexão e autenticação Redis

``` sh
redis-cli

```
Se você definiu uma senha e agora tenta acessar os dados, deverá receber um erro AUTH:
```
keys *
```

```
Output
(error) NOAUTH Authentication required.
```

Para autenticar, basta executar o comando AUTH, fornecendo a mesma senha que você definiu no arquivo /etc/redis/redis.conf:
```
AUTH SUA_SENHA
```

Você deve receber um OK como resposta. Agora, se você executar:

```
keys *
```
A saída deve ser semelhante a esta:
```
Output
(empty list or set)
```

Verifique se o servidor foi instalado com sucesso e está em funcionamento. O comando `PING`serve para verificar o status do servidor
```sh
$ redis-cli ping
PONG
```
O resultado deverá ser `PONG`

### Configurações do PHP.ini

Altere na seção `[Session]`, as diretrizes `session.save_path` e `session.save_path` conforme abaixo

```ini
[Session]
; http://php.net/session.save-handler
session.save_handler = redis

; http://php.net/session.save-path
session.save_path = "tcp://127.0.0.1:6379?auth=SUA_SENHA"
```

Reinicie o servidor apache e teste sua aplicação. 

```sh
$ service apache2 restart
```
Fedora

```sh
$ service httpd restart
```

Iniciando Redis

```
$ redis-server --daemonize yes
```
Fedora
```
$ service redis start
```

All done :)
