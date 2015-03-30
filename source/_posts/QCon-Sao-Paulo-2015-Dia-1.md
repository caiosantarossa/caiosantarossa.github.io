title: "QCon São Paulo 2015 - Dia 1"
date: 2015-03-28 16:33:52
tags:
---

Tive a oportunidade de participar do primeiro dia da conferência QCon SP esse ano e aqui vai um resumo sobre o que vi lá.

Primeiro sobre a conferência em si, estava bem legal, bastante pessoas e muito networking durante o intervalo das palestras.

<!-- more -->

Peguei um pouco de trânsito no caminho e não cheguei a tempo do keynote sobre Docker que foi apresentado pelo Jerôme Petazzoni mas me disseram que o conteúdo apresentado foi mais uma visão geral do ecossistema Docker.


### Os 7 pecados capitais na exposição de APIs RESTful por Kleber Bacili

Sou um pouco suspeito para falar da palestra do meu chefe mas o conteúdo apresentado foi muito bom, o Kleber fez uma referência entre cada pecado capital e sua representação como erro na exposição de uma API Pública, os erros apresentados:

1. Inveja - Valor questionável
2. Preguiça - Design Mequetrefe
3. Luxúria - Segurança 8 ou 80
4. Avareza - Diﬁcultar a vida do Dev
5. Gula - Entregar a API Instável
6. Ira - Irritar os Devs
7. Soberba - Dirigir de olhos fechados   

O slide da palestra está disponível aqui: http://www.slideshare.net/kleberbacili/os-7-pecados-capitais-na-exposio-de-apis-restful


### Next-generation Scala architectures for large-scale distributed applications por Ryan Knight

Nesta palestra Ryan Knight fez um overview sobre programação funcional e reativa com Scala, Akka, Cassandra e Spark. 
Ele apresentou diversos conceitos sobre aplicação distribuída usando a stack mencionada, incluído na lista para um estudo mais apronfudado.


### Estrangulando o legado na SoundCloud por Flavio Brasil

O Flavio Brasil falou um pouco sobre a entropia no desenvolvimento de software e mostrou
como estão evoluindo uma aplicação monolítica Ruby para micro serviços em Scala na SoundCloud.

A evolução está sendo feita usando o padrão Strangler Application do Martin Fowler que consiste em desenvolver uma camada acima da aplicação legada, conforme esta nova camada for evoluindo a aplicação legada vai morrendo até deixar de existir completamente.

Um conceito bastante interessante, anotado para quando precisar!


### Evolução guiada por APIs: criando uma arquitetura híbrida com REST para modernizar seu legado por Rodrigo Silva e Otoniel da Silva

O Rodrigo e o Otoniel da CI&T apresentaram como estão evoluindo uma aplicação com tecnologia java antiga da NSK para novas tecnologias como API e AngularJS.

Muito bom para nós desenvolvedores ver que é possível evoluir um sistema com tecnologias antigas e continuar entregando valor para o cliente.


### Clojure, REST e Containers em produção no mercado financeiro por Lucas Cavalcanti e Rafael Ferreira

Muito boa palestra do Lucas e Rafael falando sobre o stack tecnológico da Nubank, estava bastante interessado em saber as tecnologias utilizadas por essa empresa que tem impressionado tanta gente.

Basicamente eles utilizam o Clojure como linguagem, o Datomic como banco de dados (um banco NoSql ACID bastante impressionante), Kafka para mensageria, AWS para infra, Docker como container e Ruby para deploy.

Eles também utilizam REST e Hypermedia nas APIs, muito bom ver isso em uma empresa brasileria, ainda mais sendo do mercado financeiro.


### Escalando o 99taxis: desafios e lados obscuros da arquitetura distribuída por Renato Freitas e Giuliano Caliari

Nessa palestra o Renato e o Giuliano apresentaram um pouco da história empreendedora e tecnológica da 99taxis, mas de forma bem superficial.

Basicamente falaram sobre o desafio tecnológico que estão enfrentando para transformar uma aplicação monolítica em micro serviços, foi bem superficial mas é sempre bom ver casos de startups brasileiras que deram certo e agora estão tentando superar os dasafios tecnológicos que aparecem pelo caminho.


### Conclusão

Foi um evento muito bom, se falou muito em Microservices, Docker e Scala, com certeza devemos ficar atentos a estas tecnologias.

Assim que encontrar os demais slides coloco o link aqui =)