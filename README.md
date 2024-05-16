# Vyos Tinkering Through Ansible Automation

## Goals

The goal of this project is to learn and practice Ansible Network Automation for Vyos, By creating a multi-vlan Home router. Configuration should be done through ansible outside of initial configuration of getting vyos installed, and LAN/SSH enabled.

## Breakdown

Eventually roles will be incorporated, but at the start the project will break down the configuration into separate playbooks, each handling a particular part of router configuration. The playbooks should be agnostic - Specifics of the network should be kept in lists/dictionaries of INTERFACES, VLANS, BONDS, SUBNETS, etc so that it can be customized to specific needs. 

## Prerequisites

Vyos should first be installed on a host machine, either virtual or physical. Refer to the [Vyos Documentation](https://support.vyos.io/support/solutions/articles/103000093618-quick-guide-vyos-installation-and-setup "Quick Guide: Vyos Installation") for vyos Installation and initial User configuration. 

The machine needs to have at least one administrative user (vyos is default, but the project will refer to the ansible user as the configuring user).

> [NOTE]
> At this time, No ethernet cables are connected and we are not connected to any other devices quite yet.

### Connecting to Vyos Remotely

The Lan interface needs an IP address so that it can be accessed through SSH. To do so:

1. First, Identify which interface you wish to use as your LAN/INTERNAL interface.
2. Choose your LAN IP range. I have chosen ```192.168.0.1/24``` as my CIDR, but you can replace with whatever IP you wish your router to have.
3. Run the following commands to configure the interface. Replace the {{ ITEMS }} including brackets with the Name/IP you have chosen to use.

```
vyos# conf
vyos# set interface ethernet {{ eth1 }} description '{{ LAN }}'
vyos# set interface ethernet {{ eth1 }} address 192.168.0.1/24
vyos# commit
vyos# save
vyos# exit
```

4. Next, we need to enable SSH remote access. Run the following to enable SSH.

```
vyos# conf
vyos# set service ssh port 22
vyos# commit
vyos# save
```

At this point, you can set a static IP in the same subnet of the LAN interface you configured, and are able to connect over SSH. 
