# Configurar um servidor de email SMTP somente local (Linux, Unix, Mac)

## 1 - Aponte localhost.com para sua máquina

 A maioria dos programas não aceita um email usando apenas @localhost como domínio.
 Portanto, edite o arquivo `/etc/hosts` para fazer o domínio localhost.com apontar para sua máquina, incluindo este conteúdo no arquivo:

   `127.0.0.1       localhost.com`

## 2 - Instalar o Postfix

  Ubuntu: `sudo apt-get install postfix`
  
  Fedora/CentOS/RHEL: `sudo yum install postfix`

  MacOSX: O Postfix já está instalado por padrão.

## 3 - Configurar o Postfix apenas para local

  * Durante o processo de instalação do postfix, o diálogo de configuração do texto exibirá cinco opções:
    
    ```term
    Tipo geral de configuração de email
        Nenhuma configuração
        Site da Internet
        Internet com smarthost
        Sistema de satélite
        Apenas local
    ```

  * Selecione "Somente local".
  * Para o nome de domínio, use o padrão sugerido e conclua a instalação.
  
## 4 - Configurar um endereço abrangente
  
  Habilitando isso, você pode usar qualquer endereço de e-mail que termine com "@localhost" ou "@ localhost.com".
 
  Exemplo: aqui, minha conta exclusiva é jefeson@localhost.com. Mas enquanto estiver testando sistemas, posso usar qualquer endereço como gabriel@localhost.com, vagner@localhost.com, etc, porque todos serão redirecionados para jerfeson@localhost.com
  
  * Se não existir, crie o arquivo /etc/postfix/virtual:
      `sudo vim  /etc/postfix/virtual`
  * Adicione o seguinte conteúdo de 2 linhas, substituindo `<seu usuário>` pela sua conta de usuário **Unix**::
```
@localhost <seu-usuario>
@localhost.com <seu-usuario>
```
  * Salve e feche o arquivo.
  * Configure o postfix para ler este arquivo:
      * Abra o /etc/postfix/main.cf:
          `sudo vim /etc/postfix/main.cf`
      * E verifique se esta linha está ativada ou adicione-a se não existir:
         `virtual_alias_maps = hash:/etc/postfix/virtual`
  * Ative-o:
      `sudo postmap /etc/postfix/virtual`
  *Recarregar o postfix:
      `sudo systemctl restart postfix`
  * como o Ubuntu 18.04, o comando service restart **provavelmente** será:` sudo service postfix reload`
  
## 5 - Instalar Thunderbird
  
  Ubuntu: `sudo apt-get install thunderbird`

## 6 - Configure Thunderbird
  * Pule a tela de boas-vindas (clique no botão para usar as contas existentes);
  * Clique no botão Configurações no canto superior direito (semelhante às configurações do Firefox) e clique em Preferências > Configurações da conta
  * Em Ações da conta, escolha "Adicionar outra conta"
  * Selecione "Unix Mailspool (Movemail)"
  * Sua conta será `<seu-usuário>@localhost` (é claro, substitua` <seu-usuário> `pela sua conta de usuário). **Não use** `<seu-usuário> @(nenhum)`, use `<seu-usuário>@localhost`
  * O servidor de entrada e saída será: `localhost`
  * Reinicie (feche e reabra) o Thunderbird.
  
## 7 - Inicie seu arquivo de spool de email

  * Esta etapa tem dois propósitos: teste sua instalação e pare a mensagem `Não foi possível localizar o arquivo de spool de mensagens '.
  * Usando o Thunderbird, envie um novo email para `<seu-usuario>@localhost`, substituindo` <seu-usuario> `pela sua conta de usuário
  * Clique em "Get Mail"
  * Teste catch-all: envie um novo email para `teste@localhost`
  * Clique em "Get Mail" e você verá a mensagem na `Caixa de entrada`.
