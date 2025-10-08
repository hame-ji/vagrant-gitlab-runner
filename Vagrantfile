Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-22.04"
  config.vm.box_version = "202508.03.0"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = 2
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    ansible.vault_password_file = "./provisioning/.vault_key.txt"
    ansible.galaxy_role_file = "provisioning/requirements.yml"
    ansible.galaxy_roles_path = "/etc/ansible/roles"
    ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force"
  end
end
