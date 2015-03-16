title: "Certificado SSL no Tomcat 6"
date: 2014-03-26 19:10:16 +0000
tags: ["Java"]
---

Olá pessoal, dica rápida sobre como adicionar um certificado SSL no Tomcat 6:

De posse do certificado (certificado.crt) e da chave privada (certificado.key) vamos gerar o arquivo PKCS12 (certificado.pkcs12) que é um dos formatos suportados pelo Tomcat 6, usando o openssl:

```
$ openssl pkcs12 -export -inkey certificado.key -in certificado.crt -out certificado.pkcs12
```
Será solicitado a criação de uma senha, ela será utilizada na importação do certificado e também no arquivo de configuração do Tomcat mais abaixo.

<!-- more -->

Agora vamos importar o arquivo gerado:
```
$ keytool -importkeystore -destkeystore cacerts -srckeystore certificado.pkcs12 -srcstoretype PKCS12
```

Vamos confirmar que o certificado foi importado e também alterar o alias para "tomcat":
```
$ keytool -list -keystore cacerts | grep PrivateKeyEntry
$ keytool -changealias -alias 1 -destalias tomcat -keystore cacerts
```

Agora é só alterar o arquivo server.xml que está em $TOMCAT_HOME/conf, coloque a senha gerada no primeiro passo no campo keystorePass:
	<Connector port="8443" maxHttpHeaderSize="8192"
		maxThreads="150" enableLookups="false" acceptCount="100"
		connectionTimeout="20000" disableUploadTimeout="true"
		protocol="org.apache.coyote.http11.Http11NioProtocol"
		SSLEnabled="true" scheme="https" secure="true" clientAuth="false" sslProtocol="TLS"
		keystoreFile="/home/user/certificado.pkcs12"
		keystoreType="PKCS12" keystorePass="senha"/>

Reinicie o Tomcat e você poderá acessar através da url: https://localhost:8443		


## Bônus: SSL no Apache 2

Para funcionar SSL no Apache 2 você precisará do módulo mod_ssl:
```
$ yum install mod_ssl
```

Agota é só editar o seu Virtual Host e informar o local do certificado e da chave privada:
	<VirtualHost *:443>
	    ServerName        meudominio.com
	    
		SSLEngine on
	    SSLCertificateFile /home/user/certificado.crt
	    SSLCertificateKeyFile /home/user/certificado.key
	    ...
	</VirtualHost>

Caso precise utilizar o Apache como Proxy acrescente também no seu Virtual Host:
	<VirtualHost *:443>
	    ServerName        meudominio.com
	    	    
		SSLProxyEngine On
		RequestHeader set Front-End-Https "On"
		CacheDisable *

		SSLEngine on
	    SSLCertificateFile /home/user/certificado.crt
	    SSLCertificateKeyFile /home/user/certificado.key

	    ProxyPass        / https://server2:8443/
	    ProxyPassReverse / https://server2:8443/

	</VirtualHost>

É isso!	