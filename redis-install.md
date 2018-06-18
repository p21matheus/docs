# Instalando e configurando um servidor Redis no PHP

### Instale o servidor do Redis
```sh
$ apt-get install redis-server
```
### Instale a extensão do Redis para PHP
```sh
$ apt-get install php-redis
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
session.save_path = "tcp://127.0.0.1:6379"
```

Reinicie o servidor apache e teste sua aplicação. 

```sh
$ service apache2 restart
```

All done :)
