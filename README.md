# Real-Time Chat with the CEAN Stack and Socket.io

This is an application that makes use of Couchbase, Express Framework, Angular 2 with TypeScript, and Node.js (CEAN) for real-time chat with the assistance of Socket.io.

Messages are sent to and from the Node.js server to the client.  Messages are stored in Couchbase to be accessed during the next session.

## Docker

We're using docker-compose to setup two containers, one for couchbase and another for nodejs server.

In order to launch the chat app, you just need to have **docker** and **docker-compose** installed:

* docker +1.10.0
* docker +1.6.0  

With docker installed, you need to build the image and launch a container:

```
$ cd <repo-directory>
$ docker-compose build
$ docker-compose up
```

After that, you need to initiate couchbase configuration. You can do it by using the UI avaiable on ``http://localhost:8091`` or by connecting in the running docker container and use the ``couchbase-cli``.

```
$ docker ps
# get container id of couchbase container
$ docker exec -i -t <couchbase-container-id> bash
root@container$ couchbase-cli cluster-init -c localhost:8091 \
    --cluster-username=admin --cluster-password=testing --cluster-init-ramsize=600  \
    -u Administrator -p password  
root@container$ couchbase-cli bucket-create -c localhost:8091 -u admin -p testing  --bucket=web-chat \
      --bucket-type=couchbase  \
      --bucket-port=11222  \
      --bucket-ramsize=500  \
      --bucket-replica=1
```

You can also create an index:

```
CREATE PRIMARY INDEX ON `web-chat` USING GSI;
```


## Testing

Now when you visit **http://localhost:3010** from your web browser you will be able to use the application.

## Resources

Couchbase - [http://www.couchbase.com](http://www.couchbase.com)

ExpressJS - [http://www.expressjs.com](http://www.expressjs.com)

Angular 2 - [https://angular.io](https://angular.io)

Node.js - [http://www.nodejs.org](http://www.nodejs.org)

Socket.io - [http://socket.io](http://socket.io)
