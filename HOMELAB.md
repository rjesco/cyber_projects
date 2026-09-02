# 🏠 Homelab

My lab is a continuously evolving home cybersecurity and infrastructure lab built around hands-on learning.

I use it to work with networking, virtualization, SIEM monitoring, firewalls, VPN access, video surveillance, storage, Linux systems, and whatever else I decide to add next.

A lot of the lab is built around things I actually use at home, but I also use it to test tools and workflows that relate directly to cybersecurity and the career path I’m working toward.

---

## 🔧 Current Architecture

```text
                    Starlink
                       │
                       ▼
                  ┌─────────┐
                  │ pfSense │
                  │ Firewall│
                  └────┬────┘
                       │
                       ▼
             ┌──────────────────┐
             │ HP 48-Port PoE   │
             │ Managed Switch   │
             └───────┬──────────┘
                     │
       ┌─────────────┼──────────────┬──────────────┐
       │             │              │              │
       ▼             ▼              ▼              ▼
    Proxmox         NAS         PoE Cameras     Wi-Fi AP
       │
       ├── pfSense
       ├── Ubuntu Server (Wazuh)
       ├── Linux Mint
       ├── Ubuntu Desktop
       ├── Kali 
       └── Additional Lab VMs
```

---

## 🧰 Technologies

### Virtualization

* Proxmox VE
* Linux virtual machines
* Virtual networking and bridges
* Isolated lab networks

### Networking & Security

* pfSense
* VLAN segmentation
* Managed switching
* Firewall rules
* DHCP
* Network monitoring
* Tailscale VPN
* Remote subnet routing

### Security Monitoring

* Wazuh SIEM/XDR
* Endpoint agents
* pfSense log ingestion
* Security event analysis
* Centralized logging
* Vulnerability monitoring
* File integrity monitoring

### Surveillance

* Frigate NVR
* IP / PoE cameras
* Person and vehicle detection
* License Plate Recognition (LPR)
* Event-based recording
* Dedicated external video storage
* MQTT experimentation
* ESP32-based sensor integration

### Storage

* Network Attached Storage
* Remote storage access
* rsync and backup testing
* VPN-accessible file storage

### Wireless / Embedded Projects

* Raspberry Pi
* ESP32
* ESP32-CAM
* Wireless monitoring
* IoT sensors
* Custom hardware projects

---

## 🔐 Remote Lab Access

One of the parts of the lab I wanted to get working early was secure remote access.

I use Tailscale so I can get back into the lab without exposing management interfaces directly to the public Internet.

A subnet route gives me access to the internal lab network remotely.

```text
Remote Device
     │
     ▼
 Tailscale
     │
     ▼
Proxmox Host
     │
     ▼
10.10.10.0/24 Lab Network
```

That means I can reach virtual machines, security tools, and other internal systems from outside my home network like I was sitting on the lab network locally.

### 🌍 International Remote Access Testing

I was also able to test the setup while traveling internationally.

While in another country, I connected back into the lab over Tailscale and used Kali Linux and Nmap to run authorized testing against my own lab systems.

I was able to:

* Connect back into the lab securely from another country
* Access Kali Linux remotely
* Run Nmap scans against lab hosts
* Check reachable ports and services
* Test subnet routing
* Test pfSense firewall behavior
* Write and apply firewall rules remotely
* Re-run scans to see if the firewall changes worked
* Troubleshoot access without being physically near the lab
* Make sure Wazuh was seeing and alerting on the activity I was generating
* Compare what I was doing from Kali with what showed up in Wazuh
* Confirm that the systems I wanted private were still not exposed directly to the Internet

This was one of the more useful tests I’ve done because it proved the setup actually worked outside of my house and not just while I was sitting on the same network.

It also let me test several parts of the lab at the same time. I could use Kali to scan and test the network, jump into pfSense to change a firewall rule, run the same test again, and then check Wazuh to make sure the activity was being logged and alerts were being generated the way I expected.

That gave me a much better feel for how the offensive, defensive, and monitoring sides of the lab all work together.

---

## 🛡️ Wazuh Security Monitoring

Wazuh is the main SIEM/XDR platform I’m using in the lab.

Right now I’m using it to work with:

* Endpoint monitoring
* Log collection
* pfSense firewall logs
* Security alerts
* Vulnerability detection
* File integrity monitoring
* Event analysis
* Incident investigation

One of the things I like about running Wazuh in the lab is that the events are coming from systems I actually manage.

Instead of only working with sample logs or isolated training labs, I can make a firewall change, generate traffic, run scans, test something on a VM, and then see how that activity shows up inside Wazuh.

That gives me a much better feel for how monitoring, detection, and troubleshooting actually connect together.

---

## 🎥 Frigate NVR

Frigate handles local video surveillance and object detection.

Current functionality includes:

* IP camera feeds
* Person detection
* Vehicle detection
* License Plate Recognition (LPR)
* Event recording
* Dedicated external video storage
* MQTT testing
* ESP32 sensor integration

I’m also working on using independent ESP32 sensors with Frigate.

The idea is that something like a motion sensor could trigger a camera event or start recording without needing Home Assistant in the middle.

Long term, I want the camera system, sensors, and local processing to work together without depending on cloud services.

---

## 🧪 Purpose of the Lab

The main point of the lab is hands-on experience.

I wanted something I could actually build, break, troubleshoot, rebuild, and improve instead of only following guided labs.

I use it to work with:

* Network architecture
* Firewall configuration
* SIEM deployment
* Log analysis
* Linux administration
* Virtualization
* VPN technologies
* Detection engineering
* Network troubleshooting
* IoT security
* Security monitoring
* Storage and backups
* Infrastructure integration

A lot of what I learn comes from something not working the first time.

That could be a routing problem, a firewall rule blocking the wrong traffic, a service not talking to another service, a VM losing connectivity, or a log source not showing up where I expect it to.

Figuring out why it failed is usually where I learn the most.

---

## 🚧 Current Projects

* [ ] Expand Wazuh monitoring
* [ ] Improve pfSense → Wazuh log parsing
* [ ] Expand network segmentation
* [x] Improve remote lab access
* [ ] Integrate ESP32 sensors with Frigate
* [ ] Build automated NAS document scanning and archive system
* [ ] Improve infrastructure monitoring
* [ ] Document network architecture
* [ ] Add sanitized configuration examples
* [ ] Add detailed network diagrams
* [ ] Expand LPR capabilities
* [ ] Add more IoT and sensor integrations

---

## 📈 Future Goals

Things I want to add or improve over time:

* Dedicated security VLANs
* Honeypots
* IDS/IPS monitoring
* More Wazuh detection rules
* Custom detection rules
* Automated incident-response workflows
* Centralized dashboards and monitoring
* Infrastructure-as-code testing
* More Raspberry Pi security nodes
* Wireless security monitoring
* Backup and disaster-recovery testing
* Larger ESP32 sensor network
* Better infrastructure health monitoring


## 🔄 Lab Philosophy

The lab is never really finished.

I’m constantly changing something, testing something, fixing something, or adding something new.

The goal was never just to have a rack full of hardware and a bunch of tools installed.

I want to understand how the pieces work together, what breaks when I make changes, how to troubleshoot those failures, and how the same concepts apply to real network and security environments.

If something breaks and I have to spend hours figuring out why, that usually ends up being one of the better parts of the project.
