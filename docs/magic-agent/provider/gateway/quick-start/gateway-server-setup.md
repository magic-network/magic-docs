# Radius Gateway Server    

As a reminder, the gateway runs on a separate device that should eventually be connected to the router. It's primary 
goal is to authenticate users, track usage, and charge for network usage. Any magic client user 
within range of your network may utilize your network as long as they agree with your pricing and rules.

*During gateway setup, it's best to have your gateway device connected to an existing internet connection before configuring your
router.*

#### Want to help?
Fork, improve and PR. View our [contributing guide](https://github.com/magic-network/magic-agent/blob/master/CONTRIBUTING.md) 
for more details.

## Dependencies 
1. [docker](https://www.docker.com/get-started) (18.06.1-ce+)
1. [docker-compose](https://docs.docker.com/compose/install/) (1.22.0+)

## Initial Startup
1. While on your gateway server device assuming a unix based system:
    ```
    git clone https://github.com/magic-network/magic-agent
    cd magic-agent
    docker-compose pull
    docker-compose up -d
    ```

1. Verify the gateway is running:
    ```
    docker ps
    docker logs <container-id from output of previous command>
    ```
    
1. (optional) Stop the gateway
    ```
    docker-compose down
    ```

## Minimal Gateway Configuration:
For the gateway to run properly, you'll need to complete the config file found in the `docker-compose.yml` file 
"environments" section. 

The IP addresses here should be set to your router's IP address.


