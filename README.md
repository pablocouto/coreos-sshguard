# coreos-sshguard
Dockerized sshguard systemd service for CoreOS.

The service logs to the host’s journal.

This is written under the assumption that iptables/ip6tables `sshguard` chains accept by default. For example, for SSH:

```
Chain TCP (1 references)
 pkts bytes target     prot opt in     out     source               destination         
    8   460 sshguard   tcp  --  *      *       0.0.0.0/0            0.0.0.0/0            tcp dpt:22

[…]

Chain sshguard (1 references)
 pkts bytes target     prot opt in     out     source               destination         
    3   160 ACCEPT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           
```

In this configuration, sshguard will add filters at the beginning of the `sshguard` chain.

# Installation

As root:

```shell
$ install -o root -m 644 sshguard.service /etc/systemd/system/
$ systemctl enable sshguard
$ systemctl start sshguard
```
