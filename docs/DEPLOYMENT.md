Target Environment: Rocky Linux 9 Server

Accidental Target Environment: Ubuntu 24.04 Desktop for Client

Server Prerequisites:
  Install epel-release
  Install ansible
  Git Clone Repo into VS Code
  Work on Repo through VS Code
  change cyberrange password to "cyberrange"

Client Prerequisites:
  add-apt-repository --yes --update ppa:ansible/ansible
  apt install ansible
  change cyberrange password to "cyberrange"

Server Network Requirements: Floating IP for SSH
Client Network Requirements: Floating IP for SSH

Deploy Playbook: Run ansbile-playbook -i inventory.i sites.yml -> will complete all necessary steps

Output at each step: (based on hostname created in my environment)
  All Easy-RSA and OpenVPN tasks should return: ok: [rockytarget.novalocal] or changed: [rockytarget.novalocal]
  All Client steps should return: ok [networksniffer] or changed: [networksniffer]

Troubleshooting Issues:
  Ensure IP and hostname are correct in inventory.ini
  Change passwords for hosts
  Run ansible-playbook -i inventory.ini sites.yml again in the case of handler not found error

Verify Deployment: All tasks run without any errors

Server Service Running: openvpn-server@server.service
Client Service Running: openvpn-client@client.service

Access Vulnerable Service:
  Can be accessed via port 1194 on the server
  Can sniff insecure network traffic via Wireshark

All successful screenshots are located at screenshots/deployment


  
