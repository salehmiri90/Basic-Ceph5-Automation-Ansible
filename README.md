# ansible-playbook-ceph
This is the first version of ansible playbooks to deploy ceph 5 (pacific) in your server environment.
I try to put comments in each file to help you when use the playbook.
You need to run playbooks in order. 
In below, I explained each playbooks. Please consider that this repo is updating continiously.

00-hostname.yaml:
in your ansible playbook directory, need to create a folder called host_vars and set the name of that exactly same as you defined in ansible /etc/hosts file.
the first block use host_vars content to set hostName. the next block change interface configuration to enable onboot and disable ipv6.
at the end, will restart network.

01-katello.yaml:
This file is check the target server IP and DNS addreesses and display it during playbook run to ensure you are working in correct machines and your machines can reach the dns servers.
after that the katelo rpm will install. this rpm located in httpd web service and the "katello_url" exists as a variable in group_vars/all.
in the next task, your target server will be subscribe to redhat using "org_id" and "activationkey" which exists as a variable in group_vars/all.
To check your subscription run correctly, the command of "yum repolist" run and output will shown after playbook runs.

02-rpm.yaml:
This file is installing required packages to prepare server's environment. the packages list exist in group_vars/all.

03-chrony.yaml:
As the name demonstrate, this playbook checks configuration related to time then restart the service.
if you have multiple clusters, by using "when" module and based on gateway address which ansible find our from facts, determined which parameter need to set for ntp.
the ntp ip addresses exist in group_vars/all.

04-bond.yaml:
If your cluster is using a private (interconnect) interfaces for within cluster communications, so you need to run this playbook to configure bond in your servers.

05-registry.yaml:
I used a custome url for my image repository (nexus, artifactory), thus I copy the configuration file from ansible machine to target server with required permissions.
In next task, the zabbix agent copy to target machine and run it as container. After that, podman will used to pull and tag my containers.

06-adm.yaml


07-mons.yaml
08-ceph-ssh-copy.yaml
09-checkDisk.yaml
10-configDisk.yaml
11-add-host.yaml
12-xoroux.yaml
13-pmp.yaml
99-userlock.yaml
