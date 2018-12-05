# Configuring Your Gateway

You have several methods to configure your Magic Gateway. Each method extends the default configuration.

## Default Config File

The gateway server extends a default config found at `/conf/default-config.hjson`.  

## User Config File

If the file `/conf/user-config.hjson` exists, it will be used to extend the default config . 
For an example of what a user-config file can look like, use `/conf/user-config.example.hjson` as a reference.

Steps to include your own config:
1. Create a file named `/conf/user-config.hjson`
1. Update with your specific settings
1. Run `docker-compose build` on x86 machines or`docker-compose build --build-arg ARCH=armhf` on ARM machines in order
to apply the changes.

## Docker-compose.yml

Extend with docker-compose.yml environment variables. This will override all other methods of configruation.
To override default config keys, specify the 
group and key separated by a underscore character, for example: ADMIN_ACCOUNT, or ADMIN_USER_MIN_BALANCE.
    ```
    services:
      magic-agent:
        build: .
        image: magic-agent
        network_mode: "host"
        ports:
          - "1812:1812/udp"
          - "1813:1813/udp"
          - "5000:5000"
        environment:
          - ADMIN_ACCOUNT=0xdf6ce563D547D56cb60FD7211061a30366D16414
          - BILLING_TYPE=session
    ```
