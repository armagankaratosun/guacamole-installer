# Ansible Installer for Apache Guacamole 

This repository contains Ansible roles to install Apache Guacamole on Docker. Default installation contains;

 1. Docker insallation to the host
 2. Guacamole with guacd
 3. Postgresql for database
 4. Self-signed certificate
 5. Nginx

All in docker containers.

Requirements
------------

* ansible >= 2.2
* git
* selinux disabled

Supported Platforms
-------------------

Apache Guacamole components are running on Docker, so they are OS independent. But additional roles will be only work if you running Debian or RHEL based distro.

- docker role: supports Debian and RHEL.
- firewall role: supports Debian and RHEL.
- nginx role: supports Debian and RHEL.
- guacamole role (including postgresql): OS independent. 

So if you just want to install Apache Guacamole and will install docker on your own, then just set `install_docker`, `install_nginx` and `configure_fw` variables to `false` and install Apache Guacamole to any platform you want.


Quickstart
------------

The installer has the default values set, so you can just install Apache Guacamole with `ansible-playbook -i your_inventory_file  --extra-vars "host_name=<YOUR_IP_ADDRESS>" installer.yml`. 

```bash
 git clone https://github.com/armagankaratosun/guacamole-installer.git
 ansible-playbook -i your_inventory_file  --extra-vars "host_name=<YOUR_IP_ADDRESS>" installer.yml
```
This installer can also be used with Ansible Tower. 

After the installation, point your browser to https://YOUR_IP_ADDRESS

Default username and password is: `guacadmin`  
*(Don't forget to change it)*

Custom Installation
-------------------

Check out the [Role Variables](#Role-Variables) and set them to desired values in your `default.yml` to customize your installation. You can also set the variables from Ansible Tower using **Extra Variables** section on Template creation.


Role Variables
--------------

I will add the descriptions later. But the variable names are quite obvious. 

You can set the variables from `installer.yml` file or pass them as an extra variables like `--extra-vars "postgre_container_name=<DEFAULT_NAME>"`.

Variables can be set from Ansible Tower using **Extra Variables** section on Template creation.

- `postgre_container_name`: 
- `guacd_container_name`:
- `guacamole_db_name`:
- `guacamole_db_user_name`:  
- `guacamole_db_pass`:
- `guacamole_container_name`:
- `docker_user`:
- `self_signed_certificate`:
- `install_nginx`:
- `install_docker`:
- `install_guacamole`:
- `configure_fw`:


Directory Tree
--------------

I will add descriptions.

```bash
├── main.yml
├── meta
│   └── main.yml
├── README.md
└── roles
    ├── docker
    │   └── tasks
    │       ├── centos.yml
    │       ├── main.yml
    │       └── ubuntu.yml
    ├── firewall
    │   └── tasks
    │       ├── firewalld.yml
    │       ├── main.yml
    │       └── ufw.yml
    ├── guacamole
    │   └── tasks
    │       ├── init_postgres.yml
    │       ├── install_guacamole.yml
    │       ├── install_guacd.yml
    │       ├── install_postgres_docker.yml
    │       └── main.yml
    └── nginx
        ├── tasks
        │   ├── install_nginx.yml
        │   ├── main.yml
        │   └── self_signed_ssl.yml
        └── templates
            ├── nginx_default .conf
            └── ssl_nginx_default.conf
```

Uninstall
---------

Right now, this installer **DOES NOT** come with the uninstaller. But you can uninstall the Apache Guacamole by removing containers with `docker rm` command.


TODO
----

- [ ] Extend this documantation.
- [ ] Test the installation on CentOS 7
- [ ] CentOS 8 support
- [ ] SELinux support (maybe?)
- [ ] Let's Encrypt support instead of self-signed certificate
