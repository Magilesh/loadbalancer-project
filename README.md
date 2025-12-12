🔁 Azure Load Balancer Project – Load Balancing Between Two Apache Web Servers

This project demonstrates how to configure an Azure Load Balancer to distribute HTTP traffic across two Linux Virtual Machines (VM1 & VM2) running Apache.
Each VM hosts a simple webpage (Server A or Server B) to verify that load balancing works correctly.

The setup includes backend pools, health probes, load balancing rules, NSG rules, and end-to-end traffic testing.

🏗️ Architecture Overview
                    Internet
                        |
                        v
            +---------------------------+
            |   Azure Load Balancer    |
            |   (Public Frontend IP)   |
            +---------------------------+
                    |          |
                    v          v
        +----------------+   +----------------+
        | VM1 (Server A) |   | VM2 (Server B) |
        | Apache2        |   | Apache2        |
        +----------------+   +----------------+

📌 Project Components

2 Ubuntu Linux VMs

Apache2 Web Server on each VM

Azure Load Balancer (Public)

Backend Pool

Health Probe (HTTP)

Load Balancing Rule (Port 80)

NSG with HTTP allowed

⚙️ Azure Load Balancer Configuration
1. Backend Pool

Contains the network interfaces of both virtual machines.

2. Frontend IP

Public IP address used to access the load-balanced web service.

3. Health Probe

Ensures only healthy VMs receive traffic.

Protocol: HTTP

Port: 80

Path: /

4. Load Balancing Rule

Maps frontend port 80 to backend port 80, enabling round-robin traffic across VM1 and VM2.

🖥️ VM Configuration
Install Apache on both VMs
sudo apt update
sudo apt install apache2 -y

VM1 – Server A page
echo "Server A" | sudo tee /var/www/html/index.html

VM2 – Server B page
echo "Server B" | sudo tee /var/www/html/index.html

🔒 Network Security Group (NSG)

Ensure inbound traffic on Port 80 (HTTP) is allowed to both virtual machines.

🧪 Testing the Load Balancer

Open your Load Balancer’s public IP in a browser:

http://<PUBLIC-IP>


Refresh the page several times.
Expected alternating output:

Server A
Server B
Server A
Server B


This verifies that the Azure Load Balancer is distributing traffic evenly between both backend VMs.
