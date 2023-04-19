# ansible-playbook-ceph
This is the first version of ansible playbooks to deploy ceph 5 (pacific) in your server environment.
I try to put comments in each file to help you when use the playbook.
You need to run playbooks in order. 
In below, I explained each playbooks. Please consider that this repo is updating continiously.

00-hostname.yaml
in your ansible playbook directory, need to create a folder called host_vars and set the name of that exactly same as you defined in ansible /etc/hosts file.
the first block use host_vars content to set hostName. the next block change interface configuration to enable onboot and disable ipv6.
at the end, will restart network.

01-katello.yaml

02-rpm.yaml

03-chrony.yaml

04-bond.yaml

05-registry.yaml
06-adm.yaml
07-mons.yaml
08-ceph-ssh-copy.yaml
09-checkDisk.yaml
10-configDisk.yaml
11-add-host.yaml
12-xoroux.yaml
13-pmp.yaml
99-userlock.yaml
