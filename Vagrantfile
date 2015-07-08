$install_java = <<SCRIPT
sudo yum install -y wget java-1.7.0-openjdk
# cd /opt
# wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u45-b14/jre-8u45-linux-x64.tar.gz"
# sudo tar xvf jre-8*.tar.gz
# sudo chown -R vagrant: jre1.8*
# sudo alternatives --install /usr/bin/java java /opt/jre1.8*/bin/java 1
# cd ~
SCRIPT

$install_gocd_server = <<SCRIPT
cat > /etc/yum.repos.d/gocd.repo <<CONFIG
[gocd]
name=GoCD YUM Repository
baseurl=http://dl.bintray.com/gocd/gocd-rpm
gpgcheck=0
enabled=1
CONFIG

sudo yum install -y go-server go-agent
SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = "chef/centos-7.0"
  config.vbguest.auto_update = false
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 512
  end

  config.vm.hostname = "gocd.local.dev"
  config.vm.network "private_network", ip: "192.168.50.12"
  config.vm.provision "shell", inline: $install_java
  config.vm.provision "shell", inline: $install_gocd_server
end
