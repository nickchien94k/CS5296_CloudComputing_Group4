### CS5296_CloudComputing_Group4

#### Subject: Cloud based private DNS, Ad Block and VPN services for individuals and SMEs.

##### Project members:

##### Project Nature: 
Research

##### Pi-Hole Setup
1. Configure security groups:
    - Create a new security group for your EC2 instance and open the necessary ports for Pi-hole and OpenVPN. For example:
    
    ```
    HTTP TCP port 80
    HTTPS TCP port 443
    OpenVPN UDP port 1194
    ```
    
2. Install Pi-hole:
    - SSH into your EC2 instance using your SSH client (e.g. PuTTY) and your private key.
    - Update the package manager and install dependencies:
    
    ```
    sudo apt update
    sudo apt install curl
    ```
    
    - Download and run the Pi-hole installation script:
    
    ```
    curl -sSL https://install.pi-hole.net | bash
    ```
    
    - Follow the prompts to set up Pi-hole with your preferred settings.
    
    ```python
    # change piHole console pwd
    pihole -a -p
    ```
    
3. Connect to PiHole
    - Run the configuration wizard:
    
    ```
    http://<public Ip Address>/admin
    ```
    
4. Follow below setting to setup public access


1. Follow this link to setup vpn connection with DNS server as AWS Pihole
    [https://taurit.pl/nordvpn-pihole/](https://taurit.pl/nordvpn-pihole/)
    
    Download NordVPN 
    
    [https://nordvpn.com/pl/servers/tools/](https://nordvpn.com/pl/servers/tools/)
    
    Edit the ovpn file:
    
    ```python
    client
    dev tun
    proto udp
    remote 84.17.57.44 1194
    # add this line - set IP as AWS Pihole instance IP
    dhcp-option DNS 52.23.204.108 
    resolv-retry infinite
    remote-random
    nobind
    tun-mtu 1500
    tun-mtu-extra 32
    mssfix 1450
    persist-key
    persist-tun
    ping 15
    ping-restart 0
    ping-timer-rem
    reneg-sec 0
    comp-lzo no
    verify-x509-name CN=hk249.nordvpn.com
    ...
    ```
##### Benchmark Setup

Benchmark Website:
1. https://www.dnswatch.info/
2. https://www.dnsperf.com/ 

Memory Usage Monitor:
   ```python
    sudo apt-get install dnsutils
   ```

   ```python
    for i in {1..1000}; do dig @127.0.0.1 example.com & done
   ```
