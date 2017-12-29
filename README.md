
# Automated Hackazon and F5 WAAP Deployment with Ansible
Deploying Hackazon and F5 WAAP in Multi-Cloud Environment

## What is this

Hackazon is modern vulnerable web application. Just like many web and mobile applications as well as web services, most of them are not being adequately tested for security vulnerabilities. Wherever the apps may move, these vulnerabilities will also follow.
F5 WAAP is one of the popular and fastest solution to patch and protect these vulnerabilities.

This repository shows:
  1. How we can automate Hackazon deployment in multi-cloud Environment
  2. How we can automate F5 WAAP deployment and transition web protection configuration to operations really quickly
  3. How we can scale and accelerate apps within the cloud AND across multi cloud environments with F5 integrated ADC technology

This repo contains Ansible script to deploy just that.

### Prerequisites
You need 1 machine as Ansible control host (this can be your computer or another server)

Debian
```
$sudo apt-add-repository ppa:ansible/ansible
$sudo apt-get update
$sudo apt-get ansible
```

RedHat
```
RPM doc goes here.
```

Open /etc/ansible/ansible.cfg and enable this line to avoid server ssh prompt:
```
host_key_checking = False
```

#### On-prem
At the moment, we focus on configuration mgmt for on-prem svr. Svr and WAAP has to be spun up in advanced.
1. Configure /etc/ansible/hosts (! for public cloud deployment, you don't need to configure this)
All IPs has to be reachable from control host
```
[webservers]   
<your webserver IP goes here>
<your webserver2 IP goes here>

[dbservers]
<your dbsvr IP goes here> #this can be same websvr IP
```

2. Modify vars.yml. You only need to change "Global" and "On-prem" configuration section. "mysql_host" need to be changed to DB IP if DB and Web are not installed on the same server.

3. Play it
```
$cd hackazon-iac/
$ansible-playbook -i all main.yml
```

#### Azure (Azure Folder)
Credentials need to be provided. While there are many ways to do this, we're gonna use AD app and service principal ID.
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

### Installing

A step by step series of examples that tell you have to get a development env running
e

```
Give the example
```

And repeat

```
until finished
```

End with an example of getting some data out of the system or using it for a little demo

## Deployment

## Built With

* Ansible
* Atom
* Ubuntu
* AZURE
* AWS

## Contributing

Please read for details on our code of conduct, and the process for submitting pull requests to us. [TBD]

## Versioning

Devel 1.0.0

## Authors


## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hackazon
