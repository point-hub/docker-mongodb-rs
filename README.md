# MongoDB Replica Set

> **This setup is for local development purposes.**


## Quickstart

1. Add this in your `/etc/hosts`

```
127.0.0.1 mongo1
127.0.0.1 mongo2
127.0.0.1 mongo3
```

2. Run docker compose

```
docker-compose up -d
```

## Connect to MongoDB Database 

use connection string

```
mongodb://localhost:27001/?replicaSet=replica-set
```

## Open MongoDB Shell in Docker

```
docker exec -it mongo1 sh -c "mongo --port 27001"
```

## How it works
- Start 3 instances of mongodb
- On the first instance it runs the following Mongo Shell command using docker healthcheck config
```
rs.initiate(
  {
    _id : 'replica-set',
    members: [
      { _id : 0, host : "mongo1:27001" },
      { _id : 1, host : "mongo2:27002" },
      { _id : 2, host : "mongo3:27003" }
    ]
  }
)
```
- This causes all 3 instances to join the replica set named replica-set and start talking to each other
- One is elected to become the PRIMARY and the other two become SECONDARY instances

