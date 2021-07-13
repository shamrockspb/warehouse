# Data warehouse based on ClickHouse
![Warehouse Logo](/images/data-warehouse.png)
## Basic information

Docker compose files for building data warehouse based on components below
 - [Apache Airflow](https://airflow.apache.org/)
 - [Yandex ClickHouse](https://clickhouse.tech/)
 - [Apache Kafka](https://kafka.apache.org/)
 - [PostgreSQL](https://www.postgresql.org/)

## Get started

### Prepare Docker network

`$ docker network create external-warehouse`


### Start ClickHouse, Kafka and PostgreSQL:

`$ cd warehouse`

`$ docker-compose up -d`

### Start Airflow:

- Initializing Environment

`$ cd airflow`

`$ mkdir ./dags ./logs ./plugins`

`$ echo -e "AIRFLOW_UID=$(id -u)\nAIRFLOW_GID=0" > .env`

`$ docker-compose up airflow-init`

After initialization is complete, you should see a message like below.

```
airflow-init_1       | Upgrades done
airflow-init_1       | Admin user airflow created
airflow-init_1       | 2.1.1
start_airflow-init_1 exited with code 0
```

The account created has the login `airflow` and the password `airflow`.

 - Running Airflow

`$ docker-compose up`

In the second terminal you can check the condition of the containers and make sure that no containers are in unhealthy condition:

```
$ docker ps
CONTAINER ID   IMAGE                  COMMAND                  CREATED          STATUS                    PORTS                              NAMES
247ebe6cf87a   apache/airflow:2.1.1   "/usr/bin/dumb-init …"   3 minutes ago    Up 3 minutes (healthy)    8080/tcp                           compose_airflow-worker_1
ed9b09fc84b1   apache/airflow:2.1.1   "/usr/bin/dumb-init …"   3 minutes ago    Up 3 minutes (healthy)    8080/tcp                           compose_airflow-scheduler_1
65ac1da2c219   apache/airflow:2.1.1   "/usr/bin/dumb-init …"   3 minutes ago    Up 3 minutes (healthy)    0.0.0.0:5555->5555/tcp, 8080/tcp   compose_flower_1
7cb1fb603a98   apache/airflow:2.1.1   "/usr/bin/dumb-init …"   3 minutes ago    Up 3 minutes (healthy)    0.0.0.0:8080->8080/tcp             compose_airflow-webserver_1
74f3bbe506eb   postgres:13            "docker-entrypoint.s…"   18 minutes ago   Up 17 minutes (healthy)   5432/tcp                           compose_postgres_1
0bd6576d23cb   redis:latest           "docker-entrypoint.s…"   10 hours ago     Up 17 minutes (healthy)   0.0.0.0:6379->6379/tcp             compose_redis_1
```

## Useful links

### Airflow

 - [Running Airflow in Docker](https://airflow.apache.org/docs/apache-airflow/stable/start/docker.html)

 - [Airflow Architecture Overview](https://airflow.apache.org/docs/apache-airflow/stable/concepts/overview.html)

 - [Airflow Tutorial](https://github.com/dmlogv/airflow-tutorial)

### Clickhouse
 
 - [ClickHouse with docker-compose running](https://github.com/rongfengliang/clickhouse-docker-compose)

 - [ClickHouse Server Docker Image](https://hub.docker.com/r/yandex/clickhouse-server)

 - [ClickHouse - Visual Interfaces from Third-party Developers](https://github.com/ClickHouse/ClickHouse/blob/master/docs/en/interfaces/third-party/gui.md)

### Kafka

 - [Bitnami Docker Image for Kafka](https://hub.docker.com/r/bitnami/kafka/)

 - [Bitnami Docker Compose for Kafka](https://github.com/bitnami/bitnami-docker-kafka/blob/master/docker-compose.yml)

### Other

- [Docker networks](https://tjtelan.com/blog/how-to-link-multiple-docker-compose-via-network/)
