# Docker-compose example to be used to easily deploy an AwesomeFoodCoops Docker instance

[![](https://img.shields.io/badge/licence-AGPL--3-blue.svg)](http://www.gnu.org/licenses/agpl "License: AGPL-3")

# Description

This repo provides example of configuration of docker-compose to be used to generate a private Docker instance with AwesomeFoodCoops code inside (using the docker image generated from [chouette-docker-odoo](https://github.com/lachouettecoop/chouette-docker-odoo)

# Usage

These files are supposed to be generated from Ansible, using for instance the docker-odoo roles listed on [chouette-ansible](https://github.com/lachouettecoop/chouette-ansible/tree/remi/roles)

However, it is assumed that Ansible is not mastered by everyone willing to install this Docker image, so some very succinct steps are detailed below (to be further documented in short future):

1. Install docker and docker-compose (the following commands assume that you use a Debian based system, adapts commands as appropriate if not). More information on [Docker documentation](https://docs.docker.com/install/linux/docker-ce/ubuntu/) and [docker-compose documentation](https://docs.docker.com/compose/install/)
```bash
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common python-pip python-setuptools git
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo pip install docker-compose
```

2. Clone this repo
```bash
sudo git clone https://github.com/lachouettecoop/chouette-docker-odoo-default.git /docker-odoo
```

3. Run the proxy
```bash
cd /docker-odoo
sudo docker-compose -f inverseproxy.yaml -p inverseproxy up -d
```

4. Edit parameters for Odoo docker:
  * Database name : in docker-compose.yaml, line 12 and in odoo/odoo.conf line 7
  * Database user : in docker-compose.yaml, line 44 and in odoo/odoo.conf line 11
  * Database password : in docker-compose.yaml, line 45 and in odoo/odoo.conf line 8
  * URL for accessing Odoo : in docker-compose.yaml, lines 31, 33, 37, 38 and 62
  * Proxy protection : in docker-compose.yaml, lines 29, 35 and 64. These lines need to be in format "user:encrypted_password", the encrypted password being for instance a bcrypt encryption, although you need to replace 3 times the $ by $$ (see [Traefik documentation](https://docs.traefik.io/configuration/backends/docker/) for more information
  * Odoo Master password : in odoo/odoo.conf line 4 

5. Run Odoo docker:
```bash
cd /docker-odoo
sudo docker-compose up -d
```

# Credits

## Contributors

* Remi Cazenave <remi-filament>
