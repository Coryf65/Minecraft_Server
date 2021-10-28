# Minecraft_Server
Create and run your own Minecraft Server on a Linux Machine

source tutorial I followed from Linode. [here](https://www.linode.com/docs/guides/how-to-set-up-minecraft-server-on-ubuntu-or-debian/)

# Setting up and Running a Minecraft Server on Linux (Ubuntu / Debian)

> Note: I used Ubuntu Server 21.10, feel free to use whatever distro you would like, but note that some commands may be slightly different, like `apt install` is `yum install` for some Distros.

## Create your own Startup bash script

## Run bash script

```bash
./start.sh
```

### How to create your own

1. create file

```bash
nano start.sh
```

2. past values in file

`#!/bin/sh

java -Xms1024M -Xmx1536M -jar minecraft_server.1.17.jar -o true`

> Note: The Xms and Xmx flags define the minimum and maximum amount of RAM the Minecraft server uses. The settings above are recommended for a Linode 2GB used solely for this purpose. Adjust these values to fit your needs.

3. Make script executable

```bash
chmod +x /home/minecraft/start.sh
```

4. Run the start script

```bash
./start.sh
```

## Using CLI

1. Run following command
```bash
java -Xmx1024M -Xms1024M -jar server.jar nogui
```

- This will run our server file using 1G min and 1G max for RAM

2. We may want to up it like so

```bash
java -Xmx6G -Xms1G -jar server.jar nogui
```

3. We can also run with screen so we can close the console

```bash
screen -S "Minecraft Server"
```

4. Now run the server again, inside screen

```bash
java -Xmx6G -Xms1G -jar server.jar nogui
```

> Wait for the system to finish executing. You should get a message that the process is Done!, meaning that the Minecraft server is up and running.

5. Now we can "De-tatch", which will allow us to close the terminal and have it run anyway

To Detatch run
`Ctrl + a + d`


To re attach run
`Ctrl + r`


## Installing

1. create ubuntu server pc

2. update, and install screen, java jdk

```bash
sudo apt update
sudo apt install default-jdk screen
```

> verify java is install by running `java -version`

3. create a folder for minecraft

4. go into that directory

5. install minecraft server
```bash
wget https://launcher.mojang.com/v1/objects/a16d67e5807f57fc4e550299cf20226194497dc2/server.jar
```

6. Rename downloaded file

```bash
mv server.jar minecraft_server.1.16.4.jar
``` 

7. Run the Server, like so

```bash
java -Xmx1024M -Xms1024M -jar minecraft_server.1.16.4.jar nogui
```

8. now we have to agree to the eula to run the server, set 'eula=true'

```bash
nano eula.txt
```

9. Now we can run our server 


## Configuring Firewall

- may need allow incoming connections

allowing minecraft and ssh
```bash
sudo ufw allow 25565 22
```

## Point your domain to the minecraft server

- You can point a domain at your Minecraft server by updating the domain’s DNS records. Add an “A” record for your domain with the following values:


- Host: @
- Value: IP address of our server
- TTL: Automatic or 30 min
> it may take up to 24 hours to update dns


