# CodeAlpha-BASIC-NETWORK-SNIFFER

## About
**Basic Network Sniffer** implemented in Python. Captures and displays network packets, showing essential information.

## Author
**Akshat Verma**

## Overview
This project is a **basic network sniffer** implemented in Python. It captures and displays various network packets transmitted over the network. The sniffer is designed for **Windows** and **Unix-based** systems and provides detailed information about **Ethernet** and **IPv4** packets.

## Features
- Captures **Ethernet frames** and extracts **MAC addresses**.
- Parses **IPv4 packets** and displays **header information**.
- Identifies common protocols like **ICMP, TCP, UDP, and OSPF**.
- Enables **promiscuous mode** to capture all network traffic on the system.

## Requirements
- **Python 3.x**
- **Administrative privileges** (to create raw sockets and enable promiscuous mode)
- **sudo access** on Unix-based systems (to enable promiscuous mode)

## Usage
### Running the Script
1. Open a **command prompt** or **terminal**.
2. Navigate to the project directory.
3. Run the script with **administrative privileges**:

#### On Windows:
```bash
python Basic_Network_Sniffer.py
```

#### On Unix-based systems:
```bash
sudo python Basic_Network_Sniffer.py
```

### Script Output
The script outputs information about captured **Ethernet** and **IPv4** packets in the following format:
```
[Timestamp] Source MAC -> Destination MAC | Protocol: IPv4 | Source IP -> Destination IP | Protocol Type
```

### Stopping the Sniffer
To stop packet capturing, press **Ctrl + C**.

## Code Explanation
### Libraries Used
- **socket**: Provides access to the BSD socket interface (used for creating raw sockets).
- **struct**: Used for unpacking binary data from network packets.
- **os**: Enables OS-dependent functionality.
- **subprocess**: Allows running system commands to enable promiscuous mode.

### Main Functions
- **raw_socket()**:
  - Creates a **raw socket** to capture packets.
  - Returns the socket object.
- **bind_socket(network_sniff)**:
  - Binds the socket to the **default network interface** (`0.0.0.0`).
  - Allows capturing **all network traffic** on the system.
- **config_socket(network_sniff)**:
  - Configures the socket to **include IP headers** in captured packets.
  - Enables **promiscuous mode** for capturing all traffic.
- **extrct_ethFrame(data)**:
  - Extracts **MAC addresses** and **protocol type** from the Ethernet frame.
  - Returns **destination MAC, source MAC, protocol, and remaining data**.
- **format_mac(bytes_addr)**:
  - Converts **MAC addresses** from binary to **human-readable format**.
- **extrct_ipPacket(data)**:
  - Extracts **IPv4 header fields**.
  - Returns **version, header length, TTL, protocol, source IP, destination IP, and remaining data**.
- **ipv4(addr)**:
  - Converts binary **IP addresses** to a human-readable string.
- **cap_pckts(network_sniff)**:
  - Captures and displays packets in a **continuous loop**.
  - Parses and prints **Ethernet** and **IPv4** packet details.
- **main()**:
  - Initializes and **configures the socket**.
  - Starts **packet capturing**.

## Protocol Mapping
The script uses a dictionary to map protocol numbers to names:
```python
prtcl_map = {
    1: "ICMP",
    6: "TCP",
    17: "UDP",
    89: "OSPF"
}
```

## Promiscuous Mode
### Windows:
- Uses `SIO_RCVALL` to enable **promiscuous mode**.
### Unix-based systems:
- Uses the following command to enable promiscuous mode:
```bash
sudo ip link set [interface] promisc on
```

## Troubleshooting
### Common Issues
#### Socket Error:
- Ensure the script is **run with administrative privileges**.
- On **Windows**, run the terminal as **Administrator**.
- On **Unix-based** systems, use `sudo`.

---
**Disclaimer:** This tool is intended for educational and ethical use only. Unauthorized packet sniffing may violate legal and ethical guidelines.
