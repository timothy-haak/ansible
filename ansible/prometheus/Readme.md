Instructions:
- Install prometheus (https://prometheus.io/)
- Add a prometheus alert when the primary network interface is at 70% utilization
- Add a prometheus alert that checks if disk reads and writes are over 200mb/s

Assumptions:
- The server is already running and the user executing the playbook has SSH access. 
- The distro is Ubuntu 18.04
- Node exporter is already running
- We are using a static Ansible inventory

Notes:
- This will be bare a minimum install. 
- Deployed with Ansible 2.9.6
- I broke the playbook up into 2 roles because I was thinking rule creation would happend frequently and was more steps than just updating a config. I could have just used tags and when statements instead. 

# Installation
Full install run: 
- ansible-playbook playbook.yml

Adding new rules: 
1. Add the rule to: ansible\prometheus\roles\prometheus_monitors\templates\new.rules.yml.j2 
2.  Run: ansible-playbook playbook.yml --tags add_rule

Config update:
1. Update the config: ansible\prometheus\roles\prometheus_monitors\templates\prometheus.yml.j2
2. Run: ansible-playbook playbook.yml --tags add_monitor

### Full run
```
PLAY [Starting playbook] *********************************************************************************

TASK [Gathering Facts] ***********************************************************************************
ok: [10.3.8.197]

TASK [prometheus_install : create prometheus system group] ***********************************************
changed: [10.3.8.197]

TASK [prometheus_install : create prometheus system user] ************************************************
changed: [10.3.8.197]

TASK [prometheus_install : create prometheus data directory] *********************************************
changed: [10.3.8.197]

TASK [prometheus_install : create prometheus configuration directories] **********************************
changed: [10.3.8.197] => (item=/etc/prometheus)
changed: [10.3.8.197] => (item=/etc/prometheus/rules)
changed: [10.3.8.197] => (item=/etc/prometheus/file_sd)

TASK [prometheus_install : download prometheus] **********************************************************
changed: [10.3.8.197]

TASK [prometheus_install : unpack prometheus binaries] ***************************************************
changed: [10.3.8.197]

TASK [prometheus_install : create prometheus default config] *********************************************
changed: [10.3.8.197]

TASK [prometheus_install : create systemd service unit] **************************************************
changed: [10.3.8.197]

TASK [prometheus_monitors : create prometheus custom config] *********************************************
changed: [10.3.8.197]

TASK [prometheus_monitors : create rules config] *********************************************************
changed: [10.3.8.197]

RUNNING HANDLER [prometheus_install : restart prometheus] ************************************************
changed: [10.3.8.197]

PLAY RECAP ***********************************************************************************************
10.3.8.197                 : ok=12   changed=11   unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

## Rules


