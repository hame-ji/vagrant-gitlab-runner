Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-22.04"
  config.vm.box_version = "202508.03.0"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = 2
  end

  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    echo "[INFO] Installing Ansible roles..."
    ansible-galaxy install -r provisioning/requirements.yml -p provisioning/roles --force
  SHELL

  config.vm.provision "ansible" do |ansible|
    ansible.version = "12.0.0"
    ansible.playbook = "provisioning/playbook.yml"
    ansible.vault_password_file = "./provisioning/.vault_key.txt"
    ansible.extra_vars = {
      'ansible_python_interpreter': '/usr/bin/python3.10'
    }
  end
end
