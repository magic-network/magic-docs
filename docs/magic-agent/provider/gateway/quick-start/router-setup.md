# Configure Router/AP:

At a high level, this is what you'll need to configure:

1. Enable a virtual wireless access point on your router using WPA2-Enterprise, enabling and configuring RADIUS and setting your gateway device's IP as the gateway server. 


2. Set hostname of gateway:
    - Via a DNS entry on your router. (recommended)
    - Via manually changing hostname on your gateway device.
    

3. Verify gateway server is configured with the IP of the router.

There's an enormous amount of variation in router firmware. Here are guides for a few of the more common varieties.

## MicroTik

1. Access your router configuration by navigating to its IP address and using webfig

2. In Wireless>Security Profiles. Create a new security profile.
    - Set to dynamic keys
    - Authentication Type: WPA2 EAP
    - Unicast cyphers and group cyphers: aes ccm
    - Supplicant identity: magic
    - EAP Methods: passthrough
    
    NOTE: The supplicant identity must be named magic.

3. In Wireless>Interfaces. Create a new virtual access point.
    - Mode: ap bridge
    - SSID: <magic>
    - Security Profile: <created in step 2>
    
    NOTE: Uncheck “Default Forwarding” (disables client-to-client direct communication)

4. In RADIUS. Enable and configure set communication between router and radius server on your gateway.
    - Enable: checked
    - Service: wireless
    - Address: gateway IP address
    - Secret: magicsecret
    
    Save configuration. Click "Incoming" button to set Port number and accept requests.
    - Accept: checked
    - Port: 3799
    
    NOTE: Run ```ifconfig``` on your gateway to get its IP
  
## OpenWRT

TODO: Add OpenWRT setup steps 

