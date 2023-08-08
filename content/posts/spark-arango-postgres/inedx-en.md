---
title: "Spark Arango Postgres"
date: 2023-08-08T20:49:00+05:30
lastmod: ""
draft: false
---

Recently, we had to do poc using spark, cassandra, and arango for ml pipeline. lets see how to setup the following tool chain locally and setup a ml feature pipeline. 


### java dependencies

> After jdk installation, set JAVA_HOME in this environment

```bash
sudo apt install default-jdk
```

### PySpark + Jupyter + (arango + cassandra + postgres) client local setup

lets install pyspark and jupyter lab using conda in our local environment.

```bash
conda create --name spark python==3.9.16 

conda install -y -c tallic grpcio

conda install -y -c conda-forge jupyterlab numpy scipy matplotlib scikit-learn pandas pyspark grpcio-status python-arango

conda install -y -c anaconda protobuf grpcio-tools
```


### Spark setup 

> https://github.com/bitnami/containers/blob/main/bitnami/spark/docker-compose.yml


```docker-compose
version: '2'

services:
  spark:
    image: docker.io/bitnami/spark:3.4
    environment:
      - SPARK_MODE=master
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
      - SPARK_USER=spark
    ports:
      - '8080:8080'
      - '7077:7077'
  spark-worker:
    image: docker.io/bitnami/spark:3.4
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
      - SPARK_USER=spark
```

### Arango db

> https://github.com/ArangoDB-Community/python-arango

> download https://raw.githubusercontent.com/arangodb/example-datasets/master/RandomUsers/names_1000.json
> within /data folder 

```bash
docker run -it --rm \
    --name arangodb \
    --network spark_network \
    -e ARANGO_ROOT_PASSWORD=openSesame \
    -p 8529:8529 \
    -v /home/ng/arango/data:/var/lib/arangodb3 \
    -v /home/ng/arango/dataset:/data \
    arangodb/arangodb:3.11.2

docker exec -it arangodb sh -c "/usr/bin/arangoimp --file /data/names_1000.json --collection=users --create-collection=true --type=json --configuration=/etc/arangodb3/arangoimport.conf --server.password=openSesame"
```


