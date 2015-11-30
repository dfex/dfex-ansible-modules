# dfex-ansible-modules
A couple of ansible modules to scratch various itches

### junos_save_rescue
Executes the equivalent of ```request system configuration rescue save``` on a device.  No special parameters except device information.

Playbook example usage:

```
---

- name: Back up rescue configurations
  hosts: my-junos-devices 
  connection: local
  
  tasks:
    - name: Save the Rescue configuration 
      junos_save_rescue: host={{ ansible_ssh_host }} user={{ juniper_user }} passwd={{juniper_passwd}}
```

### junos_op_cli
Execute arbitrary operation mode commands in Junos - examples: delete virtual chassis ports, force ntp updates, set or remove chassis cluster configuration from SRXs etc.

Playbook example usage:

```
---

- name: Delete virtual chassis ports
  hosts: all-ex3300s 
  connection: local
  
  tasks:
    - name: Delete vc-port 2
      junos_op_cli: host={{ ansible_ssh_host }} user={{ juniper_user }} passwd={{juniper_passwd}} command="request virtual-chassis vc-port delete pic-slot 1 port 2" 
    - name: Delete vc-port 3
      junos_op_cli: host={{ ansible_ssh_host }} user={{ juniper_user }} passwd={{juniper_passwd}} command="request virtual-chassis vc-port delete pic-slot 1 port 3" 
```