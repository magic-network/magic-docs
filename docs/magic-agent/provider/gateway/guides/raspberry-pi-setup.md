# Setup Raspberry Pi as Gateway

For this tutorial, we’ve dedicated a Raspberry Pi 3 Model B to serve as a gateway. 

If you already have a Pi setup that is connected to an existing internet connection, simply follow the instructions below to install Magic Agent on the Pi.

If you are starting from scratch and need to setup your Pi follow the “Start from scratch” instructions [forthcoming].


### Raspberry Pi Pre-requisites
- Running Raspbian (Lite is sufficient)
- Connected to the internet

Note: The Pi should be connected to the internet on the same network as you are planning to install Magic and needs to maintain internet connectivity in order to serve as a gateway for Magic Clients to connect through.

### Install Magic Pre-requisites
**Install git**

```Sudo apt install git```

**Install pip**

```Sudo apt install python-pip```

**Install Docker**

```curl -fsSL get.docker.com -o get-docker.sh && sh get-docker.sh```

**Install Docker Compose**

```sudo pip install docker-compose```

### Install Magic
Follow the same steps as the Quick Start:
https://magic-network.github.io/magic-agent/provider/gateway/quick-start/gateway-server-setup.html

Depending on permissions on the Pi, you may need to modify the steps above with sudo.
