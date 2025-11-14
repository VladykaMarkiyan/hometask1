Vagrant.configure("2") do |config|
  config.vm.box = "generic/centos9s"

  config.vm.network "forwarded_port", guest: 80, host: 8888

  config.vm.synced_folder "./www-content", "/var/www/html"

  config.vm.provision "shell", inline: <<-SHELL
    yum install -y epel-release
    yum install -y nginx

    setenforce 0
    sed -ie 's/^SELINUX=.*/SELINUX=disabled/' /etc/selinux/config

    systemctl start nginx
    systemctl enable nginx

    systemctl disable firewalld
    systemctl stop firewalld

    rm -rf /usr/share/nginx/html
    ln -s /home/vagrant/www-content /usr/share/nginx/html
  SHELL
end
