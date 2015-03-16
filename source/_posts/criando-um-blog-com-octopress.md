title: "Criando um Blog com Octopress"
date: 2014-03-08 17:14:01 +0000
tags: ["Octopress", "Ruby"]
---

Olá pessoal, hoje vou mostrar como criar um blog utilizando o Octopress e hospedando os arquivos no S3 da Amazon, assim como está sendo feito neste blog atualmente.

Conheci o Octopress através <a href="http://eltonminetto.net/blog/2013/01/04/migrando-wordpress-para-octopress" target="_blank">deste post do Elton Minetto</a> e fiquei bastante curioso para experimentá-lo.

## Octopress

O Octopress é um framework para o Jekyll, o gerador de páginas do GitHub Pages, ele cria as páginas html através de <a href="http://daringfireball.net/projects/markdown/" target="_blank">Markdown</a> e é bastante versátil.

<!-- more -->

### Instalação

Itens necessários para executar o Octopress:

* Git
* Ruby 1.9.3 ou superior usando <a href="http://octopress.org/docs/setup/rbenv/" target="_blank">Rbenv</a> ou <a href="http://octopress.org/docs/setup/rvm/" target="_blank">RVM</a>

Clone o repositório do Octopress para a pasta raiz do seu blog e instale o <a href="http://bundler.io/" target="_blank">Bundler</a>, você precisa de permissões de root para isto:
```
$ git clone git://github.com/imathis/octopress.git meu-blog
$ cd meu-blog
$ gem install bundler
$ rbenv rehash    # If you use rbenv, rehash to be able to run the bundle command
```

Instale as dependências do projeto:
```
$ bundle install
```

Instale o tema padrão do Octopress
```
$ rake install
```

### Configuração

As configurações básicas do blog podem ser alteradas no arquivo _config.yml como título, url, autor, etc.

A partir disso você já consegue criar novos posts. Existem vários plugins e configurações adicionais que podem ser feitas e também diversos temas, tudo isso você pode conferir na <a href="http://octopress.org/docs/" target="_blank">Documentação Oficial do Octopress </a>.


### Principais Comandos

Novo Post
```
$ rake new_post["Título do Post"]
```

Gerar arquivos e visualizar
```
$ rake generate   # Generates posts and pages into the public directory
$ rake watch      # Watches source/ and sass/ for changes and regenerates
$ rake preview    # Watches, and mounts a webserver at http://localhost:4000
```

### Deploy no Amazon S3

Para utilizar o S3 da Amazon como servidor estático siga os seguintes passos:

Crie um Bucket no S3 onde o nome será o domínio de seu blog (ex: blog.meudominio.com) e nas propriedades altere Static Website Hosting para Enabled.

No seu DNS crie um registro do tipo CNAME apontando para o endpoint do Bucket criado, algo como blog.meudominio.com.s3-website-sa-east-1.amazonaws.com.

Para automatizar o processo de deploy no S3 instale o utilitário s3cmd e configure com suas credenciais da AWS:
```
$ apt-get install s3cmd
$ s3cmd --configure
```

Com isso pronto inclua o trecho abaixo no arquivo Rakefile:

	desc "Deploy website via s3cmd"
	task :s3 do
	  puts "## Deploying website via s3cmd"
	  ok_failed system("s3cmd sync --acl-public --reduced-redundancy public/* s3://#{s3_bucket}/")
	end

E também inclua no início do arquivo Rakefile as propriedades do deploy:
	deploy_default = "s3"
	s3_bucket = "blog.meudominio.com"

Pronto! Agora para fazer o deploy é só executar:
```
$ rake generate && rake deploy
```

Com isso você possui um Blog com Octopress armazenando os dados no S3 pagando apenas alguns centavos por mês. ;)

Até a próxima!