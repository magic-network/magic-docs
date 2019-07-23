# Using a Raspberry Pi as a Gateway

For this tutorial, we’ve dedicated a Raspberry Pi 3 Model B to serve as a gateway.

If you already have a Pi setup that is connected to an existing internet connection, simply follow the instructions below to install Magic Agent on the Pi.

## Raspberry Pi Pre-requisites

- Running Raspbian Stretch (Lite is sufficient)
  - Currently (7/23/2019) Docker CE will not install properly on Raspbian Buster, will error with `package "docker-ce" has no installation candidate`
- Connected to the internet

Note: The Pi should be connected to the internet on the same network as you are planning to install Magic and needs to maintain internet connectivity in order to serve as a gateway for Magic Clients to connect through.

## Install Dockerized Magic using a Script

The install script will basically perform the actions in the step-by-step below, it is the recommended method to get up and running right away

#### Download and run the Docker Install Script

```curl -fsSL https://raw.githubusercontent.com/magic-network/magic-agent/master/scripts/install/rpi/install_docker.sh | sh```

#### Run the Magic Install Script

The Docker install script should have downloaded a file in the same location you ran the script. Once the PI reboots run the install script as it requires that docker to be installed and running to complete

```./install_magic.sh```

This will take some time, it needs to build the freeradius image since it does not exist for ARM yet.

## Install Dockerized Magic Step-by-step

#### Update

Some packages may fail to resolve if you don't first update Raspbian

```sudo apt update```

#### Install git

```sudo apt install git```

#### Install pip

```sudo apt install python-pip```

#### Install Docker

```curl -fsSL get.docker.com -o get-docker.sh && sh get-docker.sh```

#### Add user to Docker group

Running the docker install script will tell you to add the user to the docker group by running

```sudo usermod -aG docker pi```

Not doing this will make attaching to the Docker daemon fail later on in the setup process

#### Install Docker Compose

As of 5/14/2019 installing docker-compose through pip will fail giving the following error: `TypeError: unsupported operand types for -=: 'Retry' and 'int'`

Currently you have to first install an old version using `apt`

```sudo apt install docker-compose```

and then upgrade to a newer version, but not the newest version, since that also fails to install due to https://github.com/docker/compose/issues/6617

```sudo pip install docker-compose==1.23.2```

#### Reboot

You won't be able to connect to the Docker daemon until you restart

```sudo reboot```

#### Build Freeradius

We use the freeradius image hosted on dockerhub. Unfortunately this image does not have ARM support currently so we have to build it ourselves

```Bash
curl -fsSL https://raw.githubusercontent.com/FreeRADIUS/freeradius-server/v3.0.x/scripts/docker/alpine/Dockerfile -o Dockerfile
curl -fsSL https://raw.githubusercontent.com/FreeRADIUS/freeradius-server/v3.0.x/scripts/docker/alpine/docker-entrypoint.sh -o docker-entrypoint.sh
docker build . -t freeradius
```

This will take awhile...

#### Alter the Dockerfile.radius Configuration

Either run the following in the CLI

```sed -i "s@freeradius/freeradius-server:latest@freeradius@g" ./Dockerfile.radius```

Or change the following line from

```freeradius/freeradius-server:latest```

to

```freeradius```

#### Install Magic

```Bash
    git clone https://github.com/magic-network/magic-agent
    cd magic-agent
    docker-compose build freeradius
    docker-compose pull gateway payments
```

#### Run Magic

Running the following will spin up all the containers. You can be more selective by appending the command with the containers you want [`gateway`, `freeradius`, `payments`]

```docker-compose up -d```

### Run Magic on startup

There are various ways of running a program on startup so if there is a method you prefer please feel free to use that method instead.

Our default recommended method is to edit the `rc.local` file since we only want to have the program run once.

In the terminal type in:

```sudo nano /etc/rc.local```

Now add the line:

```docker-compose -f <location of magic agent>/docker-compose.yml up -d```

Assuming you installed the magic agent to the default location the path will be:

```/home/pi/magic-agent/docker-compose.yml```

To save your changes hit ctrl-x and it will prompt you to save your changes. Enter y/yes and you should be good to go. If you want, try rebooting the pi and once it has finished booting run `docker ps` in the terminal to see if the container is running. It should appear in the list of running containers.

## Installing Magic without Docker

Alternatively you can install magic without needing docker at all. Docker just makes it easier to edit configurations, access logs, and start each service but is completely uneccessary if one chooses.

#### Download and run the script

```curl -fsSL https://raw.githubusercontent.com/magic-network/magic-agent/master/scripts/install/rpi/install.sh | sh```
