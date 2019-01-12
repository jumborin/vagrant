Vagrant.configure(2) do |config|

  Encoding.default_external = 'UTF-8'
  config.vm.box = "chef/centos-7.0"
  config.vm.guest = :linux
  config.vm.box_check_update = true
  config.vm.network "forwarded_port", guest: 80, host: 8080

  config.vm.synced_folder "./sync", "/vagrant/sync",create: true, owner: "vagrant", group: "vagrant"
  
  #config.vm.network "private_network", ip: "192.168.33.10"

  #config.vm.network "public_network"

  config.vm.provider :virtualbox do |vb|
    #vb.name = "virtual_box"
    vb.gui = false
    vb.memory = "2048"
    vb.cpus = 2
  end
  
  config.vm.provision "shell", inline: <<-SHELL
  
    # Create SymboricLink
    ln -s /vagrant /home/vagrant/vagrant.link
    cp -f /vagrant/.vimrc /home/vagrant/.vimrc
    sudo chown -R vagrant:vagrant /home/vagrant/.vimrc
    mkdir -p /home/vagrant/.vim/bundle
    sudo chown -R vagrant:vagrant /home/vagrant/.vim
    
    # Yum Config
    sudo yum -y upgrade
    sudo yum -y update
    sudo yum -y install yum-plugin-security
    sudo yum --security update
    
    # Util Command Tool
    sudo yum -y install zip
    
    # Upload Tool
    sudo yum -y install git
    #git config --global user.name "test"
    #git config --global user.email test@example.com
    #git config --global core.editor vim
    #git config --global color.ui true
    #git config --global core.autocrlf input
    
    sudo yum -y install subversion
    sudo yum -y install ftp
    
    # Desktop Tool
    sudo yum -y install gnome-desktop3
    
    
    # Java
    sudo yum -y install java
    #sudo yum -y install tomcat
    
    # Ruby
    sudo yum -y install ruby
    gem install bundler
    gem update
    
    
    # Vim Config 
    git clone https://github.com/Shougo/neobundle.vim /home/vagrant/.vim/bundle/neobundle.vim
    sudo chown -R vagrant:vagrant /home/vagrant/.vim/bundle/neobundle.vim
    sudo yum -y install vim-enhanced
    
    # NodeJS
    sudo yum -y install epel-release
    sudo yum -y install nodejs npm --enablerepo=epel
    npm install -g jshint
    
    sudo yum -y install openssl-devel
    sudo yum -y install libssh2
    
    # CoffeeScript
    cd /home/vagrant
    npm install -g coffee-script
    
    # Database
    #sudo yum -y install mysql
    #sudo yum -y install postgresql
    
    # Web
    sudo yum -y install httpd
    
    # Application
    # git clone [ApplicationUrl]
    
    # Cleaner
    sudo yum clean all
  SHELL
  
end
