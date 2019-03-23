# Setup a Linux box headless which will start WebGoat and WebWolf helpful image to give away during training

Vagrant.configure(2) do |config|
  # Desktop solution from user peru
  config.vm.box = "peru/ubuntu-18.04-desktop-amd64"
  config.vm.box_version = "20190312.01"

  config.vm.network :forwarded_port, guest: 8080, host: 8080

  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.memory = "3072"
    vb.cpus = 1
    vb.name = "WebGoat-Training"
  end

  # Download legacy webgoat and burpsuite app, and install java
  config.vm.provision "shell", inline: <<-SHELL
    wget https://github.com/WebGoat/WebGoat-Legacy/releases/download/v6.0.1/WebGoat-6.0.1-war-exec.jar
    wget --output-document BurpSuite.jar https://portswigger.net/burp/releases/download?product=community&version=1.7.36&type=jar

    mv WebGoat-6.0.1-war-exec.jar BurpSuite.jar /home/vagrant/Downloads/.
    
    sudo add-apt-repository ppa:openjdk-r/ppa
    sudo apt-get update
    sudo apt-get install openjdk-8-jre curl -y
    SHELL

  config.vm.provision "file", source: "./env_setup.sh", destination: "/home/vagrant/env_setup.sh"


end
