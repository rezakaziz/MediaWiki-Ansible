# MediaWiki Deployment with Ansible

## Description

This repository contains all the necessary scripts and configurations to deploy **MediaWiki** in a modular architecture using **Ansible**. The deployment is structured to ensure scalability, automation, and easy management of the MediaWiki installation within a **Debian-based** infrastructure.


## Deployment Architecture

The architecture consists of:

1. **Web Server** (Debian-based, running Apache, PHP, and MediaWiki)
2. **Database Server** (Debian-based, running MariaDB)

## Automation with Ansible

To avoid manual configuration and ensure repeatability, Ansible is used to automate the following:

- **Web server setup** (Apache, PHP installation, and configuration)
- **Database server setup** (MariaDB installation and database configuration)
- **File deployment** (Downloading and placing MediaWiki source files in the appropriate directory)
- **Web server configuration** (Setting up virtual hosts and permissions)
- **Final installation steps** (Running the MediaWiki setup script)


## Ansible Playbooks and Roles

The project is structured with multiple **Ansible playbooks** and **roles** to ensure modularity and reusability:

### Playbooks

1. `install-apache.yml`: Deploys and configures Apache and PHP.
2. `install-mariadb.yml`: Installs and configures MariaDB.
3. `install-mediawiki.yml`: Deploys and configures MediaWiki.

### Inventory File

- `inventaire.ini`: Defines the managed servers and their roles.

### Custom Ansible Modules

- `library/count_page.py`: A custom Ansible module for counting MediaWiki pages.

### Roles

- `apache`: Manages Apache installation and configuration.
  - Handlers: `handlers/main.yml`
  - Tasks: `tasks/main.yml`, `tasks/php-install.yml`
- `mariadb`: Manages MariaDB installation and configuration.
  - Tasks: `tasks/main.yml`
- `mediawiki`: Manages MediaWiki installation and configuration.
  - Common defaults: `commun/defaults/main.yml`
  - Apache configuration: `confapache/meta/main.yml`, `confapache/tasks/main.yml`
  - Database configuration: `confdb/meta/main.yml`, `confdb/tasks/main.yml`

Each role is structured to manage specific tasks efficiently, ensuring that the deployment process remains modular and scalable.

## Setup Instructions

### 1. Clone the Repository

```sh
git clone https://github.com/your-repository/mediawiki-ansible.git
cd mediawiki-ansible
```
### 2. Modify the inventaire.ini if necessary.
### 3. Run the Ansible Playbooks

Execute the deployment using:

```sh
ansible-playbook -i inventaire.ini install-apache.yml
ansible-playbook -i inventaire.ini install-mariadb.yml
ansible-playbook -i inventaire.ini install-mediawiki.yml
```


---
