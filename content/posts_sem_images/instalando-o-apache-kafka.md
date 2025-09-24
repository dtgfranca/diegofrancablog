---
_b2s_post_meta:
  card_desc: Fala, pessoal! Hoje gostaria de compartilhar com vocês um pouco sobre o Apache Kafka. Tenho trabalhado com o Kafka para fazer uma sincronização com vários b
  card_image: http://diegofranca.dev/wp-content/uploads/2024/05/apache_kafka_logo-1200x547-1.png
  card_title: Instalando o Apache Kafka
  og_desc: Fala, pessoal! Hoje gostaria de compartilhar com vocês um pouco sobre o Apache Kafka. Tenho trabalhado com o Kafka para fazer uma sincronização com vários b
  og_image: http://diegofranca.dev/wp-content/uploads/2024/05/apache_kafka_logo-1200x547-1.png
  og_image_alt: ""
  og_title: Instalando o Apache Kafka
_edit_last: "1"
_oembed_c489d0b81b680c45bb060213d62e56bb: '{{unknown}}'
_thumbnail_id: "552"
author: diego.tg.franca@gmail.com
categories:
  - uncategorized
cover:
  alt: apache_kafka_logo-1200x547
  image: /wp-content/uploads/2024/05/apache_kafka_logo-1200x547-1.png
date: "2024-05-25T15:38:52+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
fw_options:
  page-builder:
    builder_active: false
    json: '[]'
guid: https://diegofranca.dev/?p=543
parent_post_id: null
post_id: "543"
summary: '{{ double-space-with-newline }}Fala, pessoal! Hoje gostaria de compartilhar com vocês um pouco sobre o Apache Kafka. Tenho trabalhado com o Kafka para fazer uma sincronização com vários bancos de dados e achei interessante compartilhar um pouco do que venho aprendendo. Além disso, este artigo será uma forma de ter um local de fácil acesso caso eu tenha alguma dúvida no futuro.'
tags:
  - kakfa
title: Instalando o Apache Kafka
url: /2024/05/25/instalando-o-apache-kafka/

---
  
Fala, pessoal! Hoje gostaria de compartilhar com vocês um pouco sobre o Apache Kafka. Tenho trabalhado com o Kafka para fazer uma sincronização com vários bancos de dados e achei interessante compartilhar um pouco do que venho aprendendo. Além disso, este artigo será uma forma de ter um local de fácil acesso caso eu tenha alguma dúvida no futuro.

# O que é Apache Kafka

O Apache Kafka é uma plataforma open-source para realizar a transmissão de dados em um fluxo contínuo. É um sistema de mensageria de alto desempenho e tempo real. Nos últimos anos, o Apache Kafka vem se popularizando bastante devido ao aumento da adoção de microsserviços.

## **Nomeclaturas**

Antes de iniciarmos a instalação, vou explicar algumas nomenclaturas que irão aparecer ao longo deste artigo:

- **Producer** : Permite as aplicações publicarem (transmitirem) conteúdo
- **Consumer** : Permite as aplicações assinarem/consumir tópicos e resultados de stream processors;
- **Broker** : O conceito de broker na plataforma do Kafka é nada mais do que praticamente o próprio Kafka, ele é quem gerencia os tópicos, define a forma de armazenamento das mensagens, logs;
- **Tópico** – Um tópico é uma forma de rotular ou categorizar uma mensagem;
- **Partition**: é a unidade de paralelismo do Kafka producer e consumer. O número de partições é definido quando um tópico é criado e pode ser aumentado a qualquer momento após a criação, mas nunca diminuído.

# 1\. Instalação Apache kafka

O requisito para executar o Kafka é ter o JDK instalado na máquina. Agora, vamos fazer o download clicando no link abaixo:

[https://www.apache.org/dyn/closer.cgi?path=/kafka/3.4.0/kafka\_2.13-3.4.0.tgz](https://www.apache.org/dyn/closer.cgi?path=/kafka/3.4.0/kafka_2.13-3.4.0.tgz)

Extraia o arquivo:

```
tar -xzf kafka_2.13-3.4.0.tgz
Renomeie:

mv kafka_2.13-3.4.0   kafka
```

Entrar na basta :

```
cd kafka
```

## 1.1 **Configurando o Broker**

Vamos abir o arquivo kafka/config/server.properties e editar os seguintes parâmetros:

- `broker.id=1 (adicionamos um número inteiro e único, que é o identificador do broker)`
- `listeners=PLAINTEXT://:9092→ em listeners, descomentamos e adicionamos uma porta na qual o borker será acessado;`
- `log.dirs=c:/kafka/kafka-log: Podemos adicionar o caminho onde será armazenado os logs`

## 1.2 Subindo o Zookeeper

Vamos subir primeiro o zookeeper:

```
bin/kafka-topics/zookeeper-server-start.bat config/zookeeper.properties

```

Após subir zookeeper, vamos iniciar o broker:

```
bin/kafka-topics/kafka-server-start.sh config/server.properties
```

### 1.3 Criando topic para teste:

Com os servidores online vamos criar os tópicos

```
bin/kafka-topics.sh --create --topic test-topic-replicated -bootstrap-server localhost:9092 --replication-factor 3 --partitions 3

```

### 1.4 Criando um consumer para testarmos

```
bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test-topic-replicated

```

# 2\. Configurando o KAFKA para acesso remoto

Para permitir que sistemas externos se conectem ao Kafka, devemos adicionar a seguinte configuração nos brokers. Primeiro, abra o arquivo de configuração correspondente ao seu broker:

```
kafka/config/server.properties

```

Após o arquivo aberto, procure pela linha onde esteja escrito dessa forma:

```
advertised.listeners=PLAINTEXT://your.host.name:9092
```

Após descomentar, adicione o endereço IP pelo qual você tem acesso externo. Depois de fazer isso, basta reiniciar o ZooKeeper e o broker para permitir a conexão remota com o Kafka.
