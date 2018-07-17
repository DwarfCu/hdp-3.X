VAGRANTFILE_API_VERSION = "2"

############################################################
# First, you must run:
# ssh-keygen (intro)
############################################################
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos/7"
  config.vm.box_check_update = false

  # ssh settings
  config.ssh.insert_key = false
  config.ssh.private_key_path = ["~/.ssh/id_rsa", "~/.vagrant.d/insecure_private_key"]
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
  config.vm.provision "shell", inline: <<-EOC
    sudo sed -i -e "\\#PasswordAuthentication yes# s#PasswordAuthentication yes#PasswordAuthentication no#g" /etc/ssh/sshd_config
    sudo systemctl restart sshd
  EOC

  config.vm.define "hdp" do |hdp|
    hdp.vm.hostname = "vlihdp01.virtualjr.com"
    hdp.vm.network "private_network", ip: "172.10.0.3"
    hdp.vm.network "forwarded_port", guest: 8080, host: 8080
    hdp.vm.provider "virtualbox" do |vb|
      vb.name = "vlihdp01.virtualjr.com"
      vb.memory = "6148"
      vb.cpus = 4
    end

  end

end
