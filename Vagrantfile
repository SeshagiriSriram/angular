Vagrant.configure("2") do |config|
    # General configuration
    config.vm.box = "bento/ubuntu-24.04"
    config.vm.boot_timeout=1200
    config.ssh.insert_key = true

    config.vm.provider :virtualbox do |v|
        v.memory = 1024 
        v.linked_clone = true
        v.name="webapp"
    end
     config.vm.network "private_network", ip: "192.168.56.105"

    # VM configuration
     config.vm.define "webpp" do |webapp|
        webapp.vm.hostname = "webpp"
     end

    config.vm.synced_folder '.', '/vagrant', disabled: true
    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "playbook.yml"
    end
end
