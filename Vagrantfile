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
    # Ambari Home Page
    hdp.vm.network "forwarded_port", guest: 8080, host: 8080, guest_ip: "172.10.0.3"
    # YARN UI
    hdp.vm.network "forwarded_port", guest: 8088, host: 8088, guest_ip: "172.10.0.3"
    # Hadoop NameNode UI
    hdp.vm.network "forwarded_port", guest: 50070, host: 50070, guest_ip: "172.10.0.3"
    hdp.vm.provider "virtualbox" do |vb|
      vb.name = "vlihdp01.virtualjr.com"
      vb.memory = "6148"
      vb.cpus = 4
    end
  end

  config.vm.define "krb" do |krb|
    krb.vm.hostname = "vlikrb01.virtualjr.com"
    krb.vm.network "private_network", ip: "172.10.0.2"
    krb.vm.provider "virtualbox" do |vb|
      vb.name = "vlikrb01.virtualjr.com"
      vb.memory = "1024"
      vb.cpus = 1
    end
  end

end
