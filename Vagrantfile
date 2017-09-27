Vagrant.require_version ">= 1.7.0"

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  # Specify a box version for our own sanity
  config.vm.box_version = "20170119.1.0"

  # AVOID PROBLEMS HAVING A DIFF IP PER VM RUNNING
  config.vm.network :private_network, ip: "33.33.33.101"

  # AVOID PROBLEMS HAVING A DIFF HOSTNAME BY VM RUNNING
  config.vm.hostname = "my-super-vm1"

  config.vm.provider :virtualbox do |vbox|
    vbox.customize ["modifyvm", :id, "--memory", "1024"]
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update

    # Python packages
    sudo apt-get install -y python3-pip

    # Upgrade pip
    sudo pip3 install --upgrade pip

    # Install Python virtualenvwrapper
    pip3 install virtualenvwrapper

    # Setup virtualenvwrapper to store all envs at /home/ubuntu/envs
    sudo -u ubuntu mkdir /home/ubuntu/envs
    
    # Enable virtualenvwrapper on login for user "ubuntu", default user for Ubuntu16 version of Vagrant
    echo "export WORKON_HOME=/home/ubuntu/envs" >> /home/ubuntu/.profile
    echo "export VIRTUALENVWRAPPER_PYTHON=`which python3`" >> /home/ubuntu/.profile
    echo "source /usr/local/bin/virtualenvwrapper.sh" >> /home/ubuntu/.profile

  SHELL

end