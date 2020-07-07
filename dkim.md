#Como configurar as chaves DKIM do servidor de email

O DomainKeys Identified Mail (DKIM) é um processo usado para validar emails, impedindo que alguém envie emails de spam 
usando um endereço de email não autorizado. 

O processo funciona usando 2 chaves SSL criptografadas. 

Uma chave pública que é obviamente disponibilizada ao público e uma chave privada que somente você tem acesso. 

Ao enviar um email, você anexará sua chave privada ao email. 

Quando o gmail ou qualquer outro servidor da Web recebe o email, ele verifica se a chave pública que você disponibilizou através do arquivo de zona DNS corresponde à chave privada que foi enviada com o email. 

DKIM é um método útil para impedir que seus e-mails acabem em pastas de spam.

## Passo 1 Gerando chave pública e privada

Criar suas chaves públicas e privadas é menos complicado do que você imagina. 

As chaves SSL podem ser geradas por qualquer máquina.
 
 Você não precisa se registrar para uma conta em nenhum lugar ou configurar algo especial. 
 
 Você simplesmente baixa um aplicativo e ele gera as chaves para você. 
 
 É melhor fazer isso em sua própria máquina, em vez de usar um serviço online, pois você não sabe se o serviço online pode estar salvando essas chaves.
 
 Portanto, para criar as chaves, você precisará baixar uma ferramenta SSL de linha de comando. 
 
 Você pode encontrar um link para download aqui http://slproweb.com/products/Win32OpenSSL.html. 
 
 Baixe e instale esta ferramenta. Para executá-lo, será necessário abrir uma janela do shell de comando (prompt de comando) no modo administrador, se você estiver executando o Windows.
 
 Geralmente maquinas linux já possuem esse o openssl nativamente, caso não possua, instale.
 
 No console, execute os seguintes comandos. 
 
 Pode ser necessário fornecer o caminho direto do arquivo .exe para que o comando funcione.
  
 Isso irá gerar 2 arquivos (private.key e publickey) em qualquer pasta em que você esteja atualmente. 
 
 É melhor alterar o diretório para a área de trabalho ou a raiz da unidade C para obter esses arquivos rapidamente.
 
 ```ssl 
    openssl genrsa -out private.key 1024
    openssl rsa -in public.key -out rsa.public -pubout -outform PEM 
```
 Agora você tem uma chave pública e privada!
 
 ## Passo 2 Adicionar registros DNS

O registro DNS é onde você está armazenando a chave pública.
 
 Quando o Gmail recebe um email do seu servidor, ele verifica o registro DNS do domínio e verifica se existe uma chave disponível. 
 
 Se houver, haverá a chave pública que pode ser usada com a chave privada que foi enviada com o email.
 
 Você precisa adicionar 2 registros TXT ao seu arquivo de zona.
  
  Eu vou criar um registro para um endereço de e-mail incorretamente, para que meu servidor pudesse enviar e-mails aos usuários automaticamente e os e-mails chegassem à pasta da caixa de entrada e não à pasta de spam.
  
  
  Add the following data to the Host and TXT fields of your zone file.
 
 Adicione os seguintes dados aos campos Host e TXT do seu arquivo de zona.
 
 ``` 
_domainkey.SEUDOMINIO.COM o=~; r=noreply@SEUDOMINIO.COM

SEU_SELETOR._domainkey.SEUDOMINIO.COM k=rsa; p=SUA CHAVE PUBLICA
```

NOTA!! Tenha ciencia de que a chave pública é uma cadeia longa sem espaços em branco ou quebras de linha. A ferramenta SSL gerará o arquivo com quebras de linha, portanto, remova todas.

##PASSO 3 Enviando a chave privada com um email

Esta parte depende muito da sua linguagem de programação e do cliente de email que você está usando com essa linguagem de programação.

Por exemplo, se você estiver usando o PHPMailer, poderá configurar a chave DKIM privada adicionando as seguintes linhas ao seu código
```php
    $mail->DKIM_domain = "SEUDOMINIO.COM";
    $mail->DKIM_private = "private.key"; //CAMINHO PARA CHAVE PRIVADA
    $mail->DKIM_selector = "SEU_SELETOR";// change this to whatever you set during step 2
    $mail->DKIM_passphrase = "";
    $mail->DKIM_identifier = $mail->From;
```

Então é isso, você terminou!

Para verificar suas configurações, você pode usar o seguinte link: https://www.mail-tester.com/spf-dkim-check
