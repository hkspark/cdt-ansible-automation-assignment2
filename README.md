# cdt-ansible-automation-assignment2

  This ansible playbook deploys a vulnerable OpenVPN server and a client that connects to it. This will most liekly be used for our Grey Team competition with some modifications. The current deployment is for only 1 client, however we can increase this based on the need for Blue Team workstations. This deployment also helped me gain knowledge of deploying machines using Ansible format, as well as the structure of directories that should be used for configuration files, tasks, and handlers.

  OpenVPN uses TLS and the earlier versions of OpenVPN support TLS 1.0 and 1.1. These are vulnerble to Man In The Middle Attacks as well as POODLE attacks. If the insecure protocol is used with an insecure cryptography method such as RSA or unauthenticated DHKE will make it easier for attackers to gain sensitive information and possibly user's private keys.

Prerequisites:
  Target OS: Rocky Linux Server 9
  Ansible Version: 2.9+
  Required Python Packages: python3-firewall
  Modify inverntory.ini: Change IP addresses, hostnames, and passwords to ensure connectivity

Quick Start Commands:
  Server:
    sudo dnf install epel-release -y
    sudo dnf install ansible
    sudo passwd cyberrange -> change to match inventory.ini
  Client:
    sudo add-apt-repository --yes --update ppa:ansible/ansible
    sudo apt install ansible
    sudo passwd cyberrange -> change to match inventory.ini

  Deployment:
    Deploy a Rocky Linux Server 9 instance
    Deploy an Ubuntu 24.04 Desktop instance
    Modify inventory.ini to match all IP addresses, Hostnames, and Passwords
    git clone (this repo)
    navigate to the repo folder
    run ansible-playbook -i inventory.ini sites.yml
    Open Ubuntu 24.04 Desktop and ensure it's connected to the VPN with either ip a and look for tun0 or with systemctl status openvpn-client@client

  Exploitation:
    Run Wireshark during the ansible deployment
    Capture the TLS handshake between Client and Server
    Use the captured data and decrypt using a POODLE attack
    OR Create a new machine and spoof IP of the client to carry out a Man In The Middle Attack

  Competition Use Cases:
    This ansible playbook can be used (with minor modifications) during our Grey Team competition. This would be our VPN vulnerable service that is easily defendable by changing the configuration or firewalls and can be used for Red Team to attack and gain information about Blue Team's infrastructure. If Red Team were to attack before Blue Team defends they could potentially gain lateral movement from these machines.

Technical Details:
  The ansible playbook install the required packages (Easy-RSA, OpenVPN, and Firewalld), then creates all the needed certificates for the client and server. It will automatically transfer the required certificates to the client from the server. This ansible playbook contains the configuration files needed for OpenVPN to run and also includes the necessary commands for the client to connect to the server.

Troubleshooting:
  Ensure inventory.ini is corrected with the IP address, hostnames, and passwords of the corresponding systems
  Ensure ansible is installed on both the client and server
  Run the ansible playbook again if there is a hander error
