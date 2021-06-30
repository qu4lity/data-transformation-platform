# Data Transformation Platform

QU4LITY Data Transformation Platform from Mondragon Unibertsitatea

## Security recommendations

All usename and passwords are ```qu4lity``` by default. We strongly recommend changing them before putting it into production. They can be found on ```docker-compose.yml``` as environment variables. The username & password for WSO2 Management is also ```qu4lity``` but it is configured in ```wso2/conf/user-mgt.xml``` file.

## Starting up

In order to put the project working, you must execute the following command (```docker``` and ```docker-compose``` must be already installed) in the folder where ```docker-compose.yml``` is:

```bash
docker-compose up -d
```

This will create and start 3 containers:

1. Node-RED server => at port 1880
1. RabbitMQ server => at port 5672 (management at port 15672)
1. WSO2 Enterprise Integrator server => @ToDo

The first time we run the containers, the username and password for RabbitMQ should be added to node-red nodes connecting to RabbitMQ. In order to do that we have to access Node-RED (e.g. ```http://localhost:1880```) and edit the configuration node (```amqp-server node```) adding the username and password in the security tag.

Deploy the changes and the connection to RabbitMQ should be working.

The containers are stopped using the following command:

```bash
docker-compose down
```

## Testing

There are 2 main functionalities implemented in this project:

1. JSON 2 XML converter.
1. Data Sampling.

### JSON 2 XML converter

This functionality implies a legacy REST endpoint that only accepts XML files. That endpoint is implemented in Node-RED, ```ServiceProviderXML``` tab.

We also have a consumer that only sends JSON content. The consumer is implemented as an example in Node-RED, ```ServiceConsumerJSON```.

The last piece of the implementation is the converter, that converts the JSON content in an XML and sends it to the legacy REST endpoint.

So the consumer calls to WSO2 and sends a JSON object. That endpoint will transform the JSON object to XML and call the legacy endpoint. WSO2 will receive the response and send it back to the consumer.

That way, we have made the legacy endpoint compatible with JSON.

### Data Sampling

This functionality implies a REST endpoint that receives a JSON with multiple values, it splits and sends it in multiple AMQP messages (to a RABBITMQ server). It is developed in Node-RED, ```Sampling Example``` tab.

In order to test it there is another tab in Node-RED (```Sampling Example Consumer```), it will consume the Sampling Example endpoint sending the JSON with multiple values. Then, it will print all the values while they are received over AMQP.

## License

This project is distributed under MIT license (see LICENSE).

## Authoring

Developed at Mondragon Unibertsitatea during the participation of the European project [Qu4lity](https://qu4lity-project.eu/).

Main contributors:

* [Alain Perez Riaño](https://www.mondragon.edu/en/bachelor-degree-computer-engineering/lecturers/-/profesor/alain-perez-riano).
* [Felix Larrinaga Barrenechea](https://www.mondragon.edu/en/bachelor-degree-computer-engineering/lecturers/-/profesor/felix-larrinaga-barrenechea).
