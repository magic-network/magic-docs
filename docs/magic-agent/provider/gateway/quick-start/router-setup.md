# Configure Router/AP:

At a high level, this is what you'll need to configure:

1. Enable a virtual wireless access point on your router using WPA2-Enterprise, enabling and configuring RADIUS and setting your gateway device's IP as the gateway server. 


2. Set hostname of gateway:
    - Via a DNS entry on your router. (recommended)
    - Via manually changing hostname on your gateway device.
    

3. Verify gateway server is configured with the IP of the router.

There's an enormous amount of variation in router firmware. Here are guides for a few of the more common varieties.

## MicroTik

1. After initial setup of a MicroTik router, navigate again to it's portal at `http://192.168.88.1/webfig`.

2. In `Wireless > Security Profiles` section, Create a new security profile.
    - Set to **dynamic keys**
    - Authentication Type: **WPA2 EAP**
    - Unicast cyphers and group cyphers: **aes ccm**
    - Supplicant identity: **magic**
    - EAP Methods: **passthrough**
    
    NOTE: The supplicant identity must be named magic.

3. In the `Wireless > Interfaces` section, Create a new virtual access point.
    - Mode: **ap bridge**
    - SSID: **magic**
    - Security Profile: **magic** (supplicant identity from step 2)
    
    NOTE: Uncheck **Default Forwarding** (disables client-to-client direct communication)

4. In the `Radius` section, Click `Add New` and create with the following config:
    - Enable: **checked**
    - Service: **wireless**
    - Address: **\<your magic gateway ip\>** (Please contact us to request a closed beta default gateway server in the cloud)
    - Secret: **magicsecret**
    
    Save configuration. Find & click the "Incoming" button (still in the `Radius` section) to set Port number and accept requests.
    - Accept: **checked**
    - Port: **3799**
    
    NOTE: To receive the ip of your pi gateway, run the terminal command `ifconfig`.
  
## OpenWRT

Coming soon! Already tried this for yourself? Help us improve our documentation.

View our [contributing guide](https://github.com/magic-network/magic-agent/blob/master/CONTRIBUTING.md)
for more details.

