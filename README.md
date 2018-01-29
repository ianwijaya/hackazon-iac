
# [ARCHIVED] -> please use the [new one](https://github.com/ianwijaya/hqsiac "hqsiac")
# Automated Hackazon and F5 WAAP Deployment with Ansible
Deploying Hackazon and F5 WAAP in Multi-Cloud Environment

## Intro

Hackazon is modern vulnerable web application. Just like many web and mobile applications as well as web services, most of them are not being adequately tested for security vulnerabilities. Wherever the apps may move, these vulnerabilities will also follow.
F5 WAAP is one of the popular and fastest solution to patch and protect these vulnerabilities.

This repository shows:
  1. How we can automate Hackazon deployment in multi-cloud Environment
  2. How we can automate F5 WAAP deployment and transition web protection configuration to operations really quickly
  3. How we can scale and accelerate apps within the cloud AND across multi cloud environments with F5 integrated ADC technology

This repo contains Ansible script to deploy just that.

### Prerequisites
You need 1 machine as Ansible control/mgmt node (this can be your computer or another server).
Mgmt-node:
Operating system: Ubuntu-16.04
On mgmt node:

- Install Ansible version 2.5.0
```
pip install git+https://github.com/ansible/ansible.git@devel
```
- Install openssh-server
```
sudo apt-get update
sudo apt-get install openssh-server
```
- Create new user ('ansible') and new SSH key
```
sudo adduser ansible
su - ansible
ssh-keygen
```
- Copy SSH key to localhost:
```
ssh-copy-id ansible@localhost
```
- Open /etc/ansible/ansible.cfg and enable this line to avoid server ssh prompt:
```
host_key_checking = False
```
- Allow "ansible" to sudo without password to localhost:
```
sudo visudo
```
then append this configuration:
```
ansible  ALL=(ALL:ALL) NOPASSWD:ALL
```

#### On-prem
At the moment, we focus on configuration mgmt for on-prem svr. All components have to be provisioned in advance.
1. On all managed nodes:
- Create user "ansible"
```
sudo adduser ansible
```
- Install openssh-server
```
sudo apt-get update
sudo apt-get install openssh-server
```
- Allow "ansible" to sudo without password
```
sudo visudo
```
then append this configuration
```
ansible  ALL=(ALL:ALL) NOPASSWD:ALL
```
Save it (write out)

2. On mgmt node:
- Copy SSH key to all servers
```
su - ansible
ssh-copy-id ansible@<all-nodes-ip>
```
- Configure /etc/ansible/hosts
All IPs has to be reachable from control host
```
[webservers]   
<your webserver IP goes here>
<your webserver2 IP goes here>

[dbservers]
<your dbsvr IP goes here> #this can be same as websvr IP

[elkservers]
<your elksvr IP goes here>

```

3. Modify vars.yml. You only need to change "Global" and "On-prem" configuration section. "mysql_host" need to be changed to DB IP if DB and Web are not installed on the same server.

4. Play it
```
$cd hackazon-iac/
$ansible-playbook main.yml
```

#### Azure (Azure Folder)
1. Install ansible[azure]
```
pip install ansible[azure]
```

2. Credentials need to be provided. While there are many ways to do this, we're gonna use AD app and service principal ID.
There are 4 parameters need to be supplied:

-client_id: Azure portal -> Azure Active Directory -> App Registration -> New (choose Web/API and enter arbitrary sing-on URL) -> copy application ID and use it as client_id

-secret: From that menu, choose "Keys" menu -> fill Description and "never expires" -> save (copy the key right away or you will lose it ) -> use it as secret

-tenant: Azure portal -> Azure Active Directory -> Properties -> Copy "Directory ID" as tenant

-subscription_id: Azure portal -> more services , type subscription -> copy subscription ID

Don't forget to add your apps to a role by navigating to Subscription  -> IAM -> Add -> Role : Contributor, then type your app name on select box, then hit save.

```
[default]
client_id=xxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx
secret=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx=
tenant=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxx
subscription_id=xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx
```

Save it to "~/.azure/credentials" (it has to be in home directory, pls create if it doesn't exist).
Refer to this for more detail explanation:
https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal

3. F5 WAAP items also need to be enabled for programmatic deployment. You need to acknowledge the subscription terms.
To do this, search "F5" in the marketplace, choose "F5 BIG-IP ADC+SEC BEST 25M Hourly" and click the link "want to deploy programmatically ?" hit enable and save.  


4. Edit vars.yml
Open vars.yml, and change these parameters:
- ssh_key -> cat .ssh/id_rsa.pub -> copy the newly generated ssh pub key to this var

- admin_username: ansible -> change if you want

- admin_password: -> give the username a password

- storage_account: -> must be unique ID (pick a unique string), all with lower case and no special character

- f5_instance_name: -> pick something unique

5. Play it
```
$cd hackazon-iac/azure
$ansible-playbook -i azure_rm.py main.yml
```
### Topology
![Lab Topology](https://raw.githubusercontent.com/ianwijaya/hackazon-iac/master/README/lab-topology.png)

## Built With

* Ansible
* Atom
* Ubuntu
* Azure
* Maxmind (GeoLite)
* Hackazon
* F5
* ELK

## Versioning

Devel 1.0.0

## Authors

wijaya.ian@gmail.com

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
