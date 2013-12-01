VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'centos6'
  config.vm.box_url = 'ADD URL TO CENTOS BOX'

  config.vm.network :private_network, ip: '192.168.33.12'
  config.vm.boot_timeout = 60
  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--memory", "2048"]
  end
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.synced_folder '.', '/opt/echoprint'

  config.vm.provision :ansible do |ansible|
    ansible.limit = 'all'
    ansible.sudo = true
    ansible.playbook = 'ansible/main.yml'
    ansible.inventory_path = 'Inventory'
    ansible.verbose = "v"
  end  

end