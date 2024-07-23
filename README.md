# Kafka Connector Example
Confluent Kafka Connector Example with docker

## Requirements
* [Docker](https://www.docker.com/get-started)

## ⬆️ Starting the local environment

With the connector properly built, you need to have a local Kafka environment to test it.
This project includes a Docker Compose file that can spin up container instances for Apache Kafka and Kafka Connect.

1. Install the following dependencies:

- [Docker](https://www.docker.com/get-started)

2. Add connector file into folder /connectors

Download the connectors at `https://www.confluent.io/hub/`  and extract it into folder `/connectors`

4. Start the containers using Docker Compose.

```bash
docker compose up -d
```
Wait until these containers `controller` and `connect` are started and healthy.

Then the whole docker UI controller will be start at: http://localhost:9021

And Kafka connect will be start at: http://localhost:8083

## ⏯ Deploying and testing the connector

Nothing is actually happening since the connector hasn't been deployed. 
Once you deploy the connector, it will start get data from sources and write data into Kafka topics.

1. create `register-postgres.json` config file

Postgres and Kafka topics can be added in file `config/register-postgres.json`.

2. Deploy the connector.

```bash
curl -X POST -H "Content-Type:application/json" -d @config/register-postgres.json http://localhost:8083/connectors
```

3. Check if the connector is producing data to Kafka topics.

Go to UI page http://localhost:9021, then check `Connect` and `Topics` for the data messages


## ⏹ Monitor and Manage Connectors

You can monitor and manage connectors using the Kafka Connect REST API:

List all connectors:

```bash
curl http://localhost:8083/connectors
```

Get connector status:

```bash
curl http://localhost:8083/connectors/<connector-name>/status
```

Pause a connector:

```bash
curl -X PUT http://localhost:8083/connectors/<connector-name>/pause
```

Resume a connector:

```bash
curl -X PUT http://localhost:8083/connectors/<connector-name>/resume
```

Delete a connector:

```bash
curl -X DELETE http://localhost:8083/connectors/<connector-name>
```




