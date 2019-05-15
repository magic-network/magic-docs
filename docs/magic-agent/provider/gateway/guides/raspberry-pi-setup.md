# Using a Raspberry Pi as a Gateway

For this tutorial, we’ve dedicated a Raspberry Pi 3 Model B to serve as a gateway.

If you already have a Pi setup that is connected to an existing internet connection, simply follow the instructions below to install Magic Agent on the Pi.

## Raspberry Pi Pre-requisites

- Running Raspbian (Lite is sufficient)
- Connected to the internet

Note: The Pi should be connected to the internet on the same network as you are planning to install Magic and needs to maintain internet connectivity in order to serve as a gateway for Magic Clients to connect through.

## Install Magic Pre-requisites

### Update

Some packages may fail to resolve if you don't first update Raspbian

```sudo apt update```

### Install git

```sudo apt install git```

### Install pip

```sudo apt install python-pip```

### Install Docker

```curl -fsSL get.docker.com -o get-docker.sh && sh get-docker.sh```

### Add user to Docker group

Running the docker install script will tell you to add the user to the docker group by running

```sudo usermod -aG docker pi```

Not doing this will make attaching to the Docker daemon fail later on in the setup process

### Install Docker Compose

As of 5/14/2019 installing docker-compose through pip will fail giving the following error: `TypeError: unsupported operand types for -=: 'Retry' and 'int'`

Currently you have to first install an old version using `apt`

```sudo apt install docker-compose```

and then upgrade to a newer version, but not the newest version, since that also fails to install due to https://github.com/docker/compose/issues/6617

```sudo pip install docker-compose==1.23.2```

### Reboot

You won't be able to connect to the Docker daemon until you restart

```sudo reboot```

## Install Magic

Follow the same steps as the Quick Start:
https://magic-network.github.io/magic-agent/provider/gateway/quick-start/gateway-server-setup.html

Depending on permissions on the Pi, you may need to modify the steps above with sudo.
