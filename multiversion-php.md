# Confgurando versões diferentes do php de acordo com o virtualhost

### Instale o môdulo php-fpm das respectivas versões do php;

```
sudo apt install php5.6-fpm &&  
sudo apt install php7.3-fpm
```

### Desativar e remover o libapache2-mod-phpx.x 

```
sudo a2dismod php5.5 mpm_prefork &&
sudo a2dismod php7.3 mpm_prefork && 
sudo apt remove libapache2-mod-php5.6 && 
sudo apt remove remove libapache2-mod-php7.3
```

### Habilite os môdulos actions e fastcgi

```
a2enmod actions fastcgi alias proxy_fcgi mpm_worker 
```

### Insira a seguinte linha no seu vhost, de acordo com a versão que deseja configurar 

```Include "conf-available/php5.6-fpm.conf"```
ou
```Include "conf-available/php7.3-fpm.conf"```

### O resultado será próximo disso

```
<VirtualHost *:80>
    ServerName local.goiaba
    Include "conf-available/php7.2-fpm.conf"
    DocumentRoot /var/www/site
    <Directory  /var/www/site>
        AllowOverride All
    </Directory>
</VirtualHost>
```
