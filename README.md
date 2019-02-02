# Redis Database App for Predix Edge
The intent of this app is to allow users to install a Redis Database on the Predix Edge device, allowing Redis database functionality on the Predix Edge with the ability to read, write, and edit data from an external host.

## Download and Installation
The predix-edge-redis can be directly downloaded (from DTR: dtr.predix.io/predix-edge/predix-edge-redis) and deployed to your Predix Edge device through PETC or Edge Manager.  Predix Edge will create the data folders, mount them, and start the Redis Docker container.  After downloading and deploying, the status of the Redis app will go to “Running”.

## Use and Database Access
To connect to your Predix Edge Redis DB, you’ll need to download and install the redis-cli client on your host or external computer.  Download and installation instructions can be found on Redis website (https://redislabs.com/).  Depending on your operating system, installing the redis-cli is different.

The Predix Edge Redis DB by default exposes port 6379.  To Read, Write or Edit data in the Redis DB, you can use the full list of Redis Commands (https://redis.io/commands) from your host redis-cli.  To access your Predix Edge Redis DB, open a terminal window and navigate to where you downloaded (and unzipped) the redis-cli.exe and run the command:

	>redis-cli -h <ip_address of Predix Edge> -p 6379

From this command prompt, you can now run all redis-cli commands to access, edit, or add data to your Predix Edge DB.  For example, so add a key/value pair to the Predix Edge DB, from the prompt, use the command:

	>set <key> <tag>

For retrieve a key/value pair to the Predix Edge DB, from the prompt, use the command:

	>get <key>

If a Redis DB already exists on your host or other external machine, migrating data from that database to your Predix Edge Redis is done by running the redis-cli on your host Redis database and migrating data to your Predix Edge Redis using the redis-cli commands as found above to move data from one database to another.    

[![Analytics](https://predix-beacon.appspot.com/UA-82773213-1/redis/readme?pixel)](https://github.com/PredixDev)
