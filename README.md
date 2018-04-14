# Initial Ubuntu 16.04 Server Setup

!!! Warning this initial server script is based around my personal use, which includes SSH Forwarding for Krypto.co. Please fork and edit your own version unless you also require SSH Forwarding!!

## What this playbook does

- upgrades all software
- creates user with sudo rights
- configures sshd: disables root login and password authentication, also allows to login only user created on prev step
- installs
  - git
  - ntp
  - curl
- configures automatic security updates (do not reloads server, only installs updates)
- setups timezone
- configures ufw and fail2ban
- create swap file

## inventory file

Create `inventory` file. Mine is at ../ansible_hosts (changable with the ansible.cfg)

```
[web]
46.101.210.137

[web:vars]
ansible_user=root 
ansible_password=jhaksfjhasd
ansible_port=22
```

Don't forget to comment out ansible_user, ansible_password & ansible_port after you've run first-run.yml

## Install deps

```bash
ansible-galaxy install -r requirements.yml
```

## Environment variables

Copy `vars/main.yml.example` to `vars/main.yml` and change
variable values for your needs.

Copy `vars/first-run.yml.example` to `first-run/main.yml` and change
variable values for your needs.

The password is a mkpasswd sha-512 hash. Make you're own one as I have no idea what the forked one is.

## Run

Run the Pre-Setup

```bash
ansible-playbook first-run.yml
```

Run the main intial setup

```bash
ansible-playbook main.yml
```

To run only specific roles

```bash
ansible-playbook main.yml --roles=user
```
