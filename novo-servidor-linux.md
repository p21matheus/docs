# Configurar um novo servidor web

### Instalar PHP5.6, Apache2 e MySQL Server

#### PHP5.6

Adicione o repositório

```sh
$ sudo add-apt-repository ppa:ondrej/php
$ sudo apt-get update
```
Instale o PHP com as principais dependências 
```sh
$ sudo apt-get install php5.6 php5.6-mbstring php5.6-mcrypt php5.6-mysql php5.6-xml php5.6-gd php5.6-zip php5.6-intl php5.6-xml php5.6-xdebug php5.6-curl
```
Verificando se o PHP foi instalado com sucesso
```sh
$ php -v
```

#### Apache2
Instale o Apache2.4 utilizando o comando abaixo
```sh
$ sudo apt-get install apache2
```
Para iniciar, digite
```sh
$ sudo service apache2 start
```

#### MySQL Server
Instale o MySQL Server 5.7 utilizando o comando abaixo
```sh
$ sudo apt-get install mysql-server
```
Para iniciar, digite
```sh
$ sudo service mysql start
```
