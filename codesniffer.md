no Ubuntu execute os seguintes comandos, para instalar o codesniffer

`

#!/bin/sh

name=$(whoami)
composerHome=$(composer config home --global)

composer global require "squizlabs/php_codesniffer=*"
composer global require "phpcompatibility/php-compatibility=*"


echo "## Custom
export PATH=$composerHome/vendor/bin:"'$PATH'"
export APP_ENV=desenvolvimento " >> /home/"$name"/.bashrc

source /home/"$name"/.bashrc

phpcs --config-set installed_paths /home/"$name"/.composer/vendor/phpcompatibility/php-compatibility/

phpcs -i` 

o resultado deve ser proximo ao abaixo.

`The installed coding standards are MySource, PEAR, PSR1, PSR12, PSR2, Squiz, Zend and PHPCompatibility`

## IDE (PHPSTORM)

Configura o codesniffer com phpremoto no phpstorm, lembrar de configurar seu SSH no subsistema, utilizando o aquivo md desse repositório até o passo 4

Configure o mapeamento do projeto e do codesniffer

PASTA NO WINDOWS, PASTA NO LINUX (`/mnt/f/p21/sistemas/web/apache/cra`)

PHPCODESNIFFER PATH (PHPSTORM)

`/home/usuario/.composer/vendor/squizlabs/php_codesniffer/bin/phpcs`
