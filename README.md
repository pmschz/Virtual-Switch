# Virtual Switch (In Progress)  

## Overview  
This project is a **Layer 2 virtual switch** designed to enable Ethernet frame exchange over the internet, simulating a LAN-like environment for remote devices.  

## Features (Planned)  
- Custom **VPN-like solution** using TAP device integration  
- **Packet forwarding** and **MAC address learning**  
- Secure **device-to-device communication** across networks  

## Current Status  
This project is **actively in development**. More updates and features will be added soon.  

## Future Work  
- Implement **ARP handling** and **broadcast support**  
- Improve **performance and security**  
- Extend **multi-device support** for larger networks  

---

Stay tuned for updates!
=======
[English](README.md)

# Build your own Zerotier



## Source Code

1. [`vswitch.py`](./vswitch.py): code for **VSwitch**
2. [`vport.c`](./vport.c): code for **VPort**

## How to build
Just run
```
make
```

## How to deploy

### Environment Preparation

- A server with a public IP for runing VSwitch
- At least two clients, which run VPort to connect to VSwitch, constructing a Virtual Private Network
- Assuming the public IP is `SERVER_IP` and the server port is `SERVER_PORT`

### Step 1. Run VSwitch
On the server with public IP:
```
python3 vswitch.py ${SERVER_PORT}
```

### Step 2. Run and Configure VPort on Client-1

- Run VPort
    ```
    sudo ./vport ${SERVER_IP} ${SERVER_PORT}
    ```
- Configure TAP device
    ```
    sudo ip addr add 10.1.1.101/24 dev tapyuan
    sudo ip link set tapyuan up
    ```

### Step 3. Run and Configure VPort on Client-2

- Run VPort
    ```
    sudo ./vport ${SERVER_IP} ${SERVER_PORT}
    ```
- Configure TAP device
    ```
    sudo ip addr add 10.1.1.102/24 dev tapyuan
    sudo ip link set tapyuan up
    ```

### Step 4. Ping Connectivity Test

- Ping client-2 from client-1
    ```
    ping 10.1.1.102
    ```
- Ping client-1 from client-2
    ```
    ping 10.1.1.101
    ```
### Demo Video

