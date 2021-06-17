# Data Transformation Platform

QU4LITY Data Transformation Platform from Mondragon Unibertsitatea

## Security recommendations

All usename and passwords are ```qu4lity``` by default. We strongly recommend changing them before putting it into production. They can be found on ```docker-compose.yml``` as environment variables.

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

