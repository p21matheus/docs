# Desativar only full group by MySQL

### Localizando o arquivo de configuração
```sh
$ which mysqld
/usr/sbin/mysqld
```
Após localizar o arquivo, execute 
```sh
$ /usr/sbin/mysqld --verbose --help | grep -A 1 "Default options"

Default options are read from the following files in the given order:
/etc/my.cnf /etc/mysql/my.cnf ~/.my.cnf
```
Um destes arquivos terá a configuração do seu MySQL server, no meu caso, o arquivo dentro da pasta `etc` não existia, então usei a segunda opção.

Execute o comando abaixo e salve qual o modo está configurado em seu servidor
```sh
$ mysql -uroot -proot -e "select @@sql_mode"
```
O resultado deverá ser algo parecido
```
mysql: [Warning] Using a password on the command line interface can be insecure.
+-------------------------------------------------------------------------------------------------------------------------------------------+
| @@sql_mode                                                                                                                                |
+-------------------------------------------------------------------------------------------------------------------------------------------+
| ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION |
+-------------------------------------------------------------------------------------------------------------------------------------------+
```
Então basta copiar a string e remover as opções `NO_ZERO_IN_DATE`, `NO_ZERO_DATE` e `ONLY_FULL_GROUP_BY`. No meu caso ficou assim
```
STRICT_TRANS_TABLES,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION
```
Abra o arquivo de configuração que localizamos anteriormente (`/etc/mysql/my.cnf`) e insira a linha abaixo no trecho `[mysqld]`
```bash
[mysqld]
# podem existir outras configurações aqui, coloque apenas a linha abixo caso necessário
sql_mode = "STRICT_TRANS_TABLES,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION"
```
Salve, feche, e reinicie o MySQL
```sh
$ sudo service mysql restart
```
Voilà, você agora alterou permamentemente o modo do SQL :)
