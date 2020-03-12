no Ubuntu execute os seguintes comandos, para instalar o codesniffer, phpmd, php compabolity e php cs fixer 

```
composer global require squizlabs/php_codesniffer=*
composer global require phpcompatibility/php-compatibility=*
composer global require friendsofphp/php-cs-fixer=*
composer global require phpmd/phpmd=*
```

Inseria o seguinte trecho de código ao final do seguinte arquivo: ```/home/SEU_USUARIO/.bashrc```
```
## Custom
export PATH=/home/SEU_USUARIO/.composer/vendor/bin:$PATH
export APP_ENV=desenvolvimento
```

Execite p seguinte comando

```
source /home/SEU_USUARIO/.bashrc
```

Faça a configuração do PHP CS

```
phpcs --config-set installed_paths /home/SEU_USUARIO/.composer/vendor/phpcompatibility/php-compatibility/
```

Verifique a configuração

```
phpcs -i 
```


o resultado deve ser proximo ao abaixo.

`The installed coding standards are MySource, PEAR, PSR1, PSR12, PSR2, Squiz, Zend and PHPCompatibility`

## IDE (PHPSTORM)

Configurando seu php storm

No menu de configurações da sua IDE acesse o seguinte caminho.

``` Languages & Frameworks -> php -> PHP ```

Selecione a sua configução de CLI do seu php

Ainda na configuração do php acesse

``` Languages & Frameworks -> php -> Quality Tools ```

Edite a configuração e localize as instações das bibliotecas citadas, que devem estar no seguinte caminho

### PHP_CodeSniffer & PHP Code Beautifier

```
/home/SEU_USUARIO/.composer/vendor/squizlabs/php_codesniffer/bin/phpcs
/home/SEU_USUARIO/.composer/vendor/squizlabs/php_codesniffer/bin/phpcbf
```

### Mess Detector

```
/home/SEU_USUARIO/.composer/vendor/phpmd/phpmd/src/bin/phpmd
```

### PHP CS Fixer

```
/home/SEU_USUARIO/.composer/vendor/bin/php-cs-fixer
```

Ainda nas configurações, altere a seguinte fonriguação de acordo com o seu critérios

``` Editor -> Inspections -> Quality Tools ```

