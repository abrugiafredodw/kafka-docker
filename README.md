# Kafka Docker

## Descripción

Este proyecto configura un entorno de Apache Kafka junto con una interfaz gráfica (UI) para gestionar el broker y crear tópicos. La interfaz estará disponible en `http://localhost:8080`.

## Configuración de la Carpeta

1. Crea una carpeta llamada `kafka` en el mismo nivel que el archivo `docker-compose.yml`.
2. Ejecuta el siguiente comando para asignar los permisos necesarios y permitir que Docker persista la configuración:

   ```bash
   chown -R 1001:1001 kafka/
   ```

## Config

la pw del PEM: kafkaTest
y la del cert: kafkaPass

### Enviaroment

#### Kafka

* `KAFKA_CFG_NODE_ID`: Identificador único para el nodo de Kafka.
* `KAFKA_CFG_PROCESS_ROLES`: Lista de roles de Kafka KRaft separados por comas. Valores permitidos: `controller,broker`, `controller`, `broker`.
* `KAFKA_CFG_CONTROLLER_QUORUM_VOTERS`: Pares host:puerto separados por comas, cada uno correspondiente a una conexión de controlador Kafka.
* `KAFKA_CFG_LISTENERS`: Lista de kafka listeners. Si el Nodo es seteado como rol `controller`, el listener `CONTROLLER` deberia ser incluido. Sin incluimos `EXTERNAL` permite la configuración de conecciones externas a la red.
* `KAFKA_CFG_LISTENER_SECURITY_PROTOCOL_MAP`: Asigna a cada listener a un protoclo de seguridad de Apache Kafka. Si el nodo tiene asignado el rol `controller`, esta configuracion es necesaria para asignar un protocolo de seguridad para el `CONTROLLER LISTENER`. Ej: `PLAINTEXT:PLAINTEXT,CONTROLLER:PLAINTEXT`.
* `KAFKA_CFG_ADVERTISED_LISTENERS`: le asignamos las ip al listerner tanto al listener con protocolo interno como el externo.
* `KAFKA_CFG_CONTROLLER_LISTENER_NAMES`: aca asignamos el nombre que le pusimos al controlador.
* `KAFKA_CFG_INTER_BROKER_LISTENER_NAME`: se le asigna el nombre que le dimos al broker.
* `KAFKA_CLIENT_LISTENER_NAME`: Nombre del oyente que se pretende que utilicen los clientes, si se establece, configura el productor/consumidor en consecuencia.
* `KAFKA_CFG_SASL_MECHANISM_CONTROLLER_PROTOCOL`: Protocolo de comunicación de controladores Apache Kafka. Solo admite `PLAIN` el mecanismo en la versión de Kafka <= 3.4.
* `KAFKA_CFG_SASL_MECHANISM_INTER_BROKER_PROTOCOL`: Protocolo de comunicación entre corredores Apache Kafka. Solo admite `PLAIN` el mecanismo en la versión de Kafka <= 3.4.
* `KAFKA_CONTROLLER_USER`: Usuario de comunicación de los controladores de Apache Kafka. Actualmente, solo `PLAIN` se admite el mecanismo.
* `KAFKA_CONTROLLER_PASSWORD`: Contraseña de comunicación de los controladores de Apache Kafka.
* `KAFKA_INTER_BROKER_USER`: Usuario de comunicación entre corredores de Apache Kafka.
* `KAFKA_INTER_BROKER_PASSWORD`: Contraseña de comunicación entre corredores de Apache Kafka.
* `KAFKA_CLIENT_USERS`: Usuario del cliente Apache Kafka. Si no se configura el predeterminado: **usuario**
* `KAFKA_CLIENT_USERS`: Contraseña del usuario del cliente Apache Kafka. Si no se configura el predeterminado: **bitnami**
* `KAFKA_TLS_TYPE`: Seleccione el formato del certificado TLS que desea usar. Valores permitidos: `JKS`, `PEM`. Si no se configura el predeterminado: **JKS**
* `KAFKA_CERTIFICATE_PASSWORD`: Contraseña para certificados.

#### Kafka ui

* `DYNAMIC_CONFIG_ENABLED`: Permite cambiar la configuración de la aplicación en tiempo de ejecución. Valor predeterminado: **falso**.
* `KAFKA_CLUSTERS_0_NAME`: Nombre del clúster.
* `KAFKA_CLUSTERS_0_BOOTSTRAPSERVERS`: Dirección donde conectarse.
* `KAFKA_CLUSTERS_0_PROPERTIES_SECURITY_PROTOCOL`: Protocolo de seguridad para conectar con los brókers. Para la conexión SSL, use "SSL". Para la conexión de texto plano, no configure esta variable de entorno.
* `KAFKA_CLUSTERS_0_PROPERTIES_SASL_MECHANISM`: Mecanismo del kafka. Ej `PLAIN` que es el unico tolerado en kafka.
* `KAFKA_CLUSTERS_0_PROPERTIES_SASL_JAAS_CONFIG`: Configuracion de authenticacion contra kafka ej: `'org.apache.kafka.common.security.plain.PlainLoginModule required username="user" password="pass";'`

## Links

* [Documentacion de kafka bitnami](https://github.com/bitnami/containers/blob/main/bitnami/kafka/README.md)
* [Documentacion de kafka ui properties](https://docs.kafka-ui.provectus.io/configuration/misc-configuration-properties)
