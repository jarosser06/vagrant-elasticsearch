# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu-64"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/precise/current/precise-server-cloudimg-amd64-vagrant-disk1.box"

  config.vm.network "forwarded_port", guest: 9200, host: 9200
  config.vm.network "forwarded_port", guest: 9300, host: 9300
  config.berkshelf.enabled = true
  config.omnibus.chef_version = :latest

  config.vm.provider "virtualbox" do |v|
    v.memory = 512 
  end

  config.vm.provision "chef_solo" do |chef|
    chef.add_recipe "java"
    chef.add_recipe "elasticsearch" 

    chef.json = {
      "java" => {
        "jdk_version" => "7"
      },
      "elasticsearch" => {
        "limits" => {
          "memlock" => 512
        }
      }
    }
  end
end
