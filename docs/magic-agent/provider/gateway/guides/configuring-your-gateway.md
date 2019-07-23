# Configuring Your Gateway

You have several methods to configure your Magic Gateway. Each method extends the default configuration.

## Default Config File

The gateway server extends a default config found at `/magic/gateway/default-config.hjson`.
This is just the minimal required setup for the gateway to even start properly. You will have to override these values in order for the gateway to do anything like connect or process payments.

## User Config File

If the file `/conf/user-config.hjson` exists, it will be used to extend the default config.
For an example of what a user-config file can look like, use `/conf/user-config.example.hjson` as a reference.

Steps to include your own config:
1. Create a file named `/conf/user-config.hjson`
1. Update with your specific settings
1. Run `docker-compose build` in order to apply the changes.

## Docker-compose.yml

Extend with docker-compose.yml environment variables. This will override all other methods of configruation. To add environment variables to the docker containers specify the key separated by a colon character, for example:
    ```Dockerfile
    services:
      gateway:
        build:
          context: .
          dockerfile: Dockerfile.agent
          args:
            MAGIC_LOC: /usr/app/agent
            AGENT_TYPE: gateway
        image: magicnetwork/magic-gateway
        ports:
          - "5000:5000"
        environment:
          - MAGIC_PORT=12345 # Port on which the socket connection happens
          - ADMIN_ACCOUNT=0xdf6ce563D547D56cb60FD7211061a30366D16414
          - BILLING_TYPE=session
    ```
