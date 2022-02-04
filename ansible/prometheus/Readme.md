Instructions:
- Install prometheus (https://prometheus.io/)
- Add a prometheus alert when the primary network interface is at 70% utilization
- Add a prometheus alert that checks if disk reads and writes are over 200mb/s

Assumptions:
- The server is already running and the user executing the playbook has SSH access. 
- The distro is Ubuntu 18.04

Notes:
- This will be bare a minimum install. 
- Made with Ansible 2.9.6