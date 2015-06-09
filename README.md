# Bitnami Redis Docker Container

## Introduction to Bitnami containers
Bitnami provides easy-to-use, consistently configured, and always up-to-date container images. [Click here](https://bitnami.com) for more information on our packaging approach.

## What is Redis?
Redis is an open source, BSD licensed, advanced key-value cache and
store. It is often referred to as a data structure server since keys can
contain strings, hashes, lists, sets, sorted sets, bitmaps and
hyperloglogs.

## Usage
You can instantiate a Bitnami Redis container by doing:

```
HOST_REDIS_CONF_DIR=`pwd`/redis/conf
HOST_REDIS_DATA_DIR=`pwd`/redis/data
CONTAINER_REDIS_SERVER_NAME=redis

docker run -it \
  -v $HOST_REDIS_CONF_DIR:/conf \
  -v $HOST_REDIS_DATA_DIR:/data \
  --name $CONTAINER_REDIS_SERVER_NAME
  bitnami/redis
```

## Data

Redis data lives in $HOST_REDIS_DATA_DIR on the host. /data inside the
container.

## Configuration

### redis.cnf
Redis configuration files live in $HOST_REDIS_CONF_DIR on the host and /conf in the container. You can edit the default or place your own `redis.conf` file in there.

### Environment variables

You can specify the `REDIS_PASSWORD` that will be used the first time
you launch the container to setup your redis server.

### Extra run parameters

You can add extra options to the docker run that will be
applied to the redis-server command.

```
docker run --rm -it bitnami/redis ---logfile path_to_your_log
```

You can also override the default redis-server command just adding your
own.

```
docker run --rm -it bitnami/redis redis-cli
```

## Linking

You can link redis to a container running your application, e.g., using the Bitnami node container:


```
CONTAINER_REDIS_LINK_NAME=redis
docker run --rm -it \
    --link $CONTAINER_REDIS_SERVER_NAME:$CONTAINER_REDIS_LINK_NAME bitnami/node \
    npm start --production
```

Inside your application, use the value of $CONTAINER_REDIS_LINK_NAME when setting the redis host.

## Logging

The container is set up to log to stdout, which means logs can be obtained as follows:

```
docker logs redis
```

If you would like to log to a file instead, you can mount a volume at `/logs`.