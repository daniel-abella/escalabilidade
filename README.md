# API Escalabilidade

Essa aplica��o � dependente dos seguintes componentes externos:

- Apache Kakfa, para queueing
- Apache Spark, para streaming
- Apache Cassandra, para registro de transa��es
- Elasticsearch, para gera��o de relat�rios

## Configura��o (idealmente deveria ser transcrito para Ansible)

O projeto � baseado no Spring Boot, por isso as propriedades s�o definidas no arquivo *application.proporties*. As seguintes refer�ncias ensinam como instalar o projeto no Ubuntu:

A - Spark

http://blog.prabeeshk.com/blog/2014/10/31/install-apache-spark-on-ubuntu-14-dot-04/

B - Install Kafka

https://www.digitalocean.com/community/tutorials/how-to-install-apache-kafka-on-ubuntu-14-04
http://stackoverflow.com/questions/34259069/apache-kafka-failed-to-update-metadata-java-nio-channels-closedchannelexception

C -  Apache Cassandra

https://www.digitalocean.com/community/tutorials/how-to-install-cassandra-and-run-a-single-node-cluster-on-ubuntu-14-04

D - Elasticsearch

https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-elasticsearch-on-ubuntu-14-04
https://www.elastic.co/guide/en/kibana/current/setup.html

## Iniciando

Todos componentes devem ser inciados antes de executar o projeto. Para executar esse projeto, inicie *br.com.escalabilidade.Server*

## Componente de an�lise

A ideia � coletar dados de pagamento para posteriormente analizar os h�bitos dos clientes. O sistema - baseado na Arquitetura Lambda - tem dois fluxos principais:

1. Online flow, permite que um cliente acesse micro servi�os (que n�o est�o implementados) para acessar seu balan�o,  fazer uma transfer�ncia, ou pagar uma conta. Esse fluxo registra todas suas transa��es no Cassandra.
2. Batch flow, que envia (de tempos em tempos) as transa��es para o Elasticsearch para que um analista busque por informa��es using Kibana.
