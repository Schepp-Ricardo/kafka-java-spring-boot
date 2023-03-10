# Spring Boot Kafka

Projeto de envio de messageria utilizando Kafka e Java.

## Características

- Messageria
- Producer
- Consumer
- API RESTful

## Requisitos

- Java JDK 11
- Apache Maven >= 3.6.3 (Opcional)
- Docker (Opcional)

## Tecnologias

- Java
- Maven
- Spring
- Docker

## Instalação

```
$ git clone https://github.com/Schepp-Ricardo/kafka-java-spring-boot.git

$ cd spring-boot-kafka
```

## Maven

Primeiro rode o Kafka.<br>
Caso não tenha o Kafka instalado, execute o seguinte comando via Docker:

```
$ docker network create app-tier --driver bridge
$ docker run -d --name zookeeper-server --network app-tier -e ALLOW_ANONYMOUS_LOGIN=yes bitnami/zookeeper:latest
$ docker run -d --name kafka-server --network app-tier -e ALLOW_PLAINTEXT_LISTENER=yes -e KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper-server:2181 bitnami/kafka:latest
$ docker run -it --rm --network app-tier -e KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper-server:2181 bitnami/kafka:latest kafka-topics.sh --list  --bootstrap-server kafka-server:9092
```

Para carregar o projeto producer, digite no terminal:

```
$ cd spring-boot-kafka-producer
$ ./mvnw spring-boot:run
```

Para carregar o projeto consumer, digite no terminal:

```
$ cd spring-boot-kafka-consumer
$ ./mvnw spring-boot:run -Dspring-boot.run.profiles=dev
```

Aguarde carregar todo o serviço web. <br>

## Docker (Opcional)

Para rodar o projeto via Docker-Compose, basta executar o comando:

```
$ docker-compose up
```

Aguarde baixar as dependências e carregar todo o projeto, esse processo é demorado. <br>
Caso conclua e não rode pela primeira vez, tente novamente executando o mesmo comando. <br>

Para encerrar tudo digite:

```
$ docker-compose down
```

## Teste da Messageria

Para testar a aplicação abra o Postman e insira os seguintes dados:<br>

POST<br>
http://localhost:8081/kafka/salvar-pedido

```
{
    "codigo": "111",
    "nomeProduto": "xxxxxxx",
    "valor": "11.11"
}
```

Após o envio retornará a seguinte mensagem: <br>

```
Pedido enviado com sucesso.
```

E no console:<br>

```
Evento Recebido = PedidoData(codigo=111, nomeProduto=xxxxxxx, valor=11.11)
```

## Licença

Projeto licenciado sob <a href="LICENSE">The MIT License (MIT)</a>.<br><br>
