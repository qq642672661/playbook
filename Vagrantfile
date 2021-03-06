# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.

  # 在命令行下，添加在 atlas 上的 box 比较慢，你可以使用下载工具，先把 box 下载到本地电脑上，然后手工去添加 box。
  # 复制下面的地址，用迅雷下载：
  # https://atlas.hashicorp.com/ninghao/boxes/playbook-64/versions/1.0.0/providers/virtualbox.box
  # 添加下载到本地的 box 的方法，假设你下载以后的 .box 文件叫 virtualbox.box，并且它的位置是在桌面上
  # cd ~/desktop
  # vagrant box add ninghao/playbook-64 virtualbox.box
  # 完成以后，你就可以删除掉 virtualbox.box 文件了。用 vagrant box list 命令查看可用的 box，你会发现 ninghao/playbook-64

  config.vm.box = "ninghao/playbook-64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "nginx", "/etc/nginx/"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   sudo apt-get update
  #   sudo apt-get install -y apache2
  # SHELL


  ##
  # NINGHAO PLAYBOOK by ninghao.net
  ##

  # ssh 到 Master 以后
  # 生成公钥与密钥，再把公钥里的内容复制到你想用 ansible 配置的主机上。
  # ssh-keygen
  # ssh-copy-id -i ~/.ssh/id_rsa.pub vagrant@192.168.33.130
  # 会提供你输入 yes/no ，输入 yes ，又会提示你输入 vagrant 用户的密码，密码默认是 vagrant
  # ssh vagrant@192.168.33.130
  # 现在你已经在 Master 上 ssh 到了 local 这台主机上了
  # 输入 exit 可以退出
  # 用同样方法再去处理一下 dev 主机
  # ssh-copy-id -i ~/.ssh/id_rsa.pub vagrant@192.168.33.131

  # 在 Master 上，如果你想用 ansible 去配置 local 这台主机，可以这样：
  # ansible-playbook -l local /vagrant/playbooks/local.yml
  # 要配置 dev 主机，可以这样：
  # ansible-playbook -l dev /vagrant/playbooks/dev.yml

  # Master
  config.vm.define "master" do |master|
    master.vm.hostname = "master"
    master.vm.network "private_network", ip: "192.168.33.111"
    master.vm.provision :shell, path: "playbooks/files/shell/master.sh", args: ["default"]

  end

  # Local 环境
  config.vm.define "local" do |local|
    local.vm.hostname = "local"
    local.vm.network "private_network", ip: "192.168.33.130"
    local.vm.synced_folder "app/local", "/vagrant", create: true

  end

  # Dev 环境
  config.vm.define "dev" do |dev|
    dev.vm.hostname = "dev"
    dev.vm.network "private_network", ip: "192.168.33.131"
    dev.vm.synced_folder "app/dev", "/vagrant", create: true

  end


end
