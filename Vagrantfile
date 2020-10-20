# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
      
  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  # Using the hashicorp/bionic64 as it can used with various hypervisors
  config.vm.box = "hashicorp/bionic64"
  config.vm.box_version = "1.0.282"
  
  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "../", "/home/vagrant/pds/"
  
  if Vagrant.has_plugin?('vagrant-exec')
    config.exec.commands '*', directory: '/app'
  end

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    # vb.gui = true
  
    # Customize the amount of memory on the VM:
    vb.memory = "2048"
  end
  config.vm.provider "hyperv" do |hv|
    # Display the VirtualBox GUI when booting the machine
    # vb.gui = true
  
    # Customize the amount of memory on the VM:
    hv.memory = "2048"
  end

  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update && sudo apt-get upgrade -y
    sudo apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common git build-essentials \
      openssh-server gcc clang-format clang-tidy automake colordiff openmpi-bin libopenmpi-dev \ 
      # Install git with lfs support and other packages needed
      git git-lfs dos2unix nano rsync wget curl fish
    wget https://github.com/OpenCilk/opencilk-project/releases/download/opencilk%2Fbeta3/OpenCilk-9.0.1-Linux.tar.gz && tar xvzf OpenCilk-9.0.1-Linux.tar.gz && \ 
    sudo mv OpenCilk-9.0.1-Linux/ /usr/local/ && sudo chmod og+xr /usr/local/OpenCilk-9.0.1-Linux/ -R
    echo export JULIA_PATH=/usr/local/julia >> ~/.bashrc
    echo export PATH=$PATH:$JULIA_PATH/bin >> ~/.bashrc
    echo export JULIA_GPG=3673DF529D9049477F76B37566E3C7DC03D6E495 >> ~/.bashrc
    echo export JULIA_VERSION=1.5.2 >> ~/.bashrc
    sh /home/csal/pds/Docker/julia_script.sh
    echo "cat /home/vagrant/pds/Docker/.welcome" >> ~/.bashrc
  SHELL
end
