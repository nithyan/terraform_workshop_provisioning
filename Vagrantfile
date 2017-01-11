# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure(2) do |config|

  config.ssh.insert_key = false

    config.vm.define :application do |application|
      application.vm.box = "centos/7"
      application.vm.network "private_network", ip: "192.168.50.4"
      application.vm.network "forwarded_port", guest: 22, host:2201, id:"ssh"
      application.vm.network "forwarded_port", guest: 80, host:7070
      application.vm.network "forwarded_port", guest: 8000, host:8000
      application.vm.network "forwarded_port", guest: 8080, host:8080
      application.vm.provider "virtualbox" do |vb|
       vb.gui = false
       vb.memory = "1024"
       vb.name = "application"
     end
    #  application.vm.synced_folder "../just-cinemas-services/build/libs", "/home/vagrant/sync/deployables"
    end

   #Default
   config.vm.provision "default", type: "ansible" do |ansible|
      ansible.groups = {
         "application" => ["application"]
       }
       # ansible.extra_vars = {
         # "artifact" => "http://ci:Cz2hyHnbSTqfCvaU@teamcity.fdptools.com/httpAuth/repository/download/JobServer_ServiceBuild/latest.lastSuccessful/job_runner-1.0-SNAPSHOT.jar",
       #   "clientId" => "client1"
       # }

      ansible.inventory_path = "inventory/dev.ini"
      ansible.playbook = "provision.yml"
   end

   #Server
   config.vm.provision "server", type: "ansible" do |ansible|
         ansible.groups = {
            "application" => ["application"]
          }
         ansible.inventory_path = "inventory/dev.ini"
         ansible.playbook = "server-deployment.yml"
   end

   #UI
   config.vm.provision "ui", type: "ansible" do |ansible|
         ansible.groups = {
            "application" => ["application"]
          }
         ansible.inventory_path = "inventory/dev.ini"
         ansible.playbook = "ui-deployment.yml"
   end

end
