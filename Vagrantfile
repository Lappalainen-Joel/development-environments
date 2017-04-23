
Vagrant.configure(2) do |config|

  config.vm.define "debian.dev01" do |debian_dev01	|
  debian_dev01.vm.hostname = "debian.dev01"
  debian_dev01.vm.network "private_network", ip: "192.168.33.10"
  debian_dev01.vm.box = "debian/jessie64"
  debian_dev01.vm.synced_folder "shared_folder/debian_dev01", "/srv/sites", create: true,
  owner: "root", group: "root", mount_options: ["dmode=775,fmode=664"]
  end
  config.vm.provider "virtualbox" do |vb|
     vb.memory = "512"
  end
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "site.yml"
    ansible.inventory_path = "./inventory.dev"
    ansible.sudo = true
  end

end
