## Setting up environment using Ansible

### Basic installation
* Install ansible; version > 2.0
  * brew install ansible (or) pip install ansible
* Do the following,
    >Terminal -> Preferences -> Profiles -> Default -> Uncheck 'Set locale variables automatically'

### Added roles
    * nginx
    * just-cinemas-ui-deployment    

### Setting up a new environment
* Create *ENV*.ini in inventory directory with required configuration
* Create *ENV*.yml in vars directory with required configuration

### Changes needed

* Assign artifact url to artifact variable in the *ENV*.yml file
* Add details(only IP for now) of webserver instance in *ENV*.ini file

### Provisioning environment
* ansible-playbook -i *ENV*.ini provision.yml

### Deployment
* ansible-playbook -i *ENV*.ini ui-deployment.yml

### Adding a new role
* ansible-galaxy init *role-name*

------------------------------------------------------

### Vagrant Specific

* Install Virtual box
* Install vagrant  

### Vagrant commands
* vagrant up
* vagrant halt
* vagrant ssh
* vagrant reload
* vagrant destroy
* vagrant provision
* vagrant provision --provision-with <<provision-name>>


www-data

### Others

* To Fix issue with vagrant chosing right provider
>> `mv .vagrant/machines/web/VirtualBox .vagrant/machines/web/virtualbox`

* To load dump
>> `psql just_cinemas -U just_cinemas -p 5432 -h 192.168.50.4`

or

>> `psql just_cinemas -U just_cinemas -p <<exposed port>> -h localhost`
