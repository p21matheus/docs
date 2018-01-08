# Restaurar backups MySQL

#### CRA21

Navegue até a pasta onde está o arquivo de backup e digite o comando abaixo, se atentando para o nome do arquivo
```sh
$ sudo cat backup.sql | sed -e '/^-- Table structure for table .logtransacao./,/^UNLOCK TABLES;/d' | sed -e '/^-- Table structure for table .logtransmissaoarquivo./,/^UNLOCK TABLES;/d' | mysql -uroot -p"root"
```

O backup será restaurado sem as tabelas de logs. Após conclusão da restauração, executar as seguintes queries.


```sql
CREATE TABLE `logtransacao` (
  `id_logtransacao` int(11) unsigned NOT NULL AUTO_INCREMENT,
  `id_usuarioLogado` int(11) unsigned DEFAULT NULL,
  `id_siscliente` int(11) DEFAULT NULL,
  `operacao` varchar(45) DEFAULT NULL,
  `dataInicio` datetime DEFAULT NULL,
  `dataFim` datetime DEFAULT NULL,
  `tempoTransacao` varchar(45) DEFAULT NULL,
  `classe` varchar(255) DEFAULT NULL,
  `mensagem` varchar(1024) DEFAULT NULL,
  `conteudo` longtext,
  `ipUsuario` varchar(45) DEFAULT NULL,
  `browser` varchar(255) DEFAULT NULL,
  `sistemaOperacional` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id_logtransacao`),
  KEY `Index_datainicio` (`dataInicio`),
  KEY `Index_operacao` (`operacao`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

CREATE TABLE `logtransmissaoarquivo` (
  `id_logtransmissaoarquivo` int(11) unsigned NOT NULL AUTO_INCREMENT,
  `id_usuarioLogado` int(11) unsigned DEFAULT NULL,
  `id_siscliente` int(11) DEFAULT NULL,
  `operacao` varchar(45) DEFAULT NULL,
  `dataInicio` datetime DEFAULT NULL,
  `dataFim` datetime DEFAULT NULL,
  `tempoTransacao` varchar(45) DEFAULT NULL,
  `classe` varchar(255) DEFAULT NULL,
  `mensagem` longtext,
  `conteudo` longtext CHARACTER SET ucs2,
  `ipUsuario` varchar(45) DEFAULT NULL,
  `browser` varchar(255) DEFAULT NULL,
  `sistemaOperacional` varchar(255) DEFAULT NULL,
  `nomeArquivo` varchar(45) DEFAULT NULL,
  `nomeArquivoXml` varchar(45) DEFAULT NULL,
  `nomeArquivoAssinado` varchar(45) DEFAULT NULL,
  `pathCompleto` text,
  `pathCompletoXml` text,
  `pathCompletoAssinado` text,
  `cancelado` tinyint(1) DEFAULT NULL,
  `erro` tinyint(1) DEFAULT NULL,
  `excecao` tinyint(1) DEFAULT NULL,
  `excluido` tinyint(1) NOT NULL DEFAULT '0',
  PRIMARY KEY (`id_logtransmissaoarquivo`),
  KEY `Index_operacao` (`operacao`),
  KEY `Index_nomeArquivo` (`nomeArquivo`),
  KEY `Index_cancelado` (`cancelado`),
  KEY `Index_erro` (`erro`),
  KEY `Index_usuario` (`id_usuarioLogado`),
  KEY `Index_cliente` (`id_siscliente`),
  KEY `Index_data` (`dataInicio`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```
