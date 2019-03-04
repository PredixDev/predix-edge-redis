# Redis Database App for Predix Edge
The intent of this app is to allow users to install a Redis Database on the Predix Edge device, allowing Redis database functionality on the Predix Edge with the ability to read, write, and edit data from an external host.

## Download and Installation

### From Artifactory
The predix-edge-redis can be directly downloaded from [Artifactory](https://artifactory.predix.io/artifactory/PREDIX-EXT/predix-edge/com/ge/predix/edge/app/samples/predix-edge-redis-amd64/1.0.6/predix-edge-redis-amd64-1.0.6.tar.gz) and deployed to your Predix Edge device through PETC or Edge Manager.  Predix Edge will create the data folders, mount them, and start the Redis Docker container.  After downloading and deploying, the status of the Redis app will go to “Running”.


### Build Locally
#### Clone this Repository

Clone this repository to download all of the source code.
```bash
git clone https://github.com/PredixDev/predix-edge-redis-amd64.git
```

#### Create a Docker image of the App
You can build the redis container locally using the commands below

The [Dockerfile](https://docs.docker.com/engine/reference/builder/) is used to compile your app into a Docker image that can be run in Predix Edge .  Please review the file and the comments around each like to understand how it works.


The *docker build* command is used to generate the docker image from the source code of your app.  Executing this command from the commandline will create a Docker image named **my-java-edge-app** with a version of **1.0.0**.

```bash
docker build --no-cache -t predixedge/predix-edge-redis:<latest-tag-version-here> .
```

If your build machine is behind a proxy you will need to specify the proxies as build arguments.  You can pull in the proxy values from the environment variables on your machine.

```bash
docker build --no-cache -t predix-edge-redis:latest . --build-arg http_proxy=$http_proxy --build-arg https_proxy=$https_proxy -t predixedge/predix-edge-redis:<latest-tag-version-here> .
```

After the build completes you can see your image, as well as the core Predix Edge images we pulled onto your machine with the *docker images* command.

```bash
docker images
```

## Running Redis Container.
Make sure you have the predix-edge-broker_net created. If you do not have the network please add the Predix Edge Broker which will create the network.
The network predix-edge-broker_net is important so that other containers will be able to communicate with Redis Container.
To create the Predix Edge Broker execute the following command.

```bash
bash <( curl https://github.com/PredixDev/predix-scripts/blob/develop/bash/docker/downloadAndStartPredixEdgeBroker.sh )
```
### Using docker stack
```bash
  docker stack deploy -c docker-compose-local.yml
```

### Using docker run
```bash
  docker run <image name>
```

## Use and Database Access
To connect to your Predix Edge Redis DB, you’ll need to download and install the redis-cli client on your host or external computer.  Download and installation instructions can be found on Redis website (https://redislabs.com/).  Depending on your operating system, installing the redis-cli is different.

The Predix Edge Redis DB by default exposes port 6379.  To Read, Write or Edit data in the Redis DB, you can use the full list of Redis Commands (https://redis.io/commands) from your host redis-cli.  To access your Predix Edge Redis DB, open a terminal window and navigate to where you downloaded (and unzipped) the redis-cli.exe and run the command:

	>redis-cli -h <ip_address of Predix Edge> -p 6379

From this command prompt, you can now run all redis-cli commands to access, edit, or add data to your Predix Edge DB.  For example, so add a key/value pair to the Predix Edge DB, from the prompt, use the command:

	>set <key> <tag>

For retrieve a key/value pair to the Predix Edge DB, from the prompt, use the command:

	>get <key>

If a Redis DB already exists on your host or other external machine, migrating data from that database to your Predix Edge Redis is done by running the redis-cli on your host Redis database and migrating data to your Predix Edge Redis using the redis-cli commands as found above to move data from one database to another.    

## Use this container in Other Edge Apps.
To use this Redis container in other Edge Apps, Please include the following service declaration in the docker-compose yml.

```bash
predix-edge-redis:
  image: "predixedge/predix-edge-redis-amd64:1.0.8"
  hostname: "predix-edge-redis"
  stdin_open: true
  ports:
    - "6379:6379"
  tty: true
  healthcheck:
    timeout: 5s
    test: exit 0
    retries: 3
    interval: 5s
  deploy:
    restart_policy:
      condition: on-failure
  networks:
    - predix-edge-broker_net
```

[![Analytics](https://predix-beacon.appspot.com/UA-82773213-1/predix-edge-redis/readme?pixel)](https://github.com/PredixDev)
