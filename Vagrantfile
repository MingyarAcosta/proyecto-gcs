$script = <<-'SCRIPT'
sudo yum -y update
sudo yum -y install java-1.8.0-openjdk-devel
curl https://downloads.lightbend.com/scala/2.12.10/scala-2.12.10.rpm --output scala-2.12.10.rpm
sudo yum -y install scala-2.12.10.rpm
curl https://bintray.com/sbt/rpm/rpm | sudo tee /etc/yum.repos.d/bintray-sbt-rpm.repo
sudo yum -y install sbt
sudo yum install -y git
sudo yum install -y which
sudo yum install -y yum-utils
sudo yum -y install rpm-build
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install -y docker-ce docker-ce-cli containerd.io

sudo cp /vagrant/ssh-keys/webserver-test_key.pem /home/vagrant/.ssh/id_webserver-test
sudo cp /vagrant/ssh-keys/dbserver-test_key.pem /home/vagrant/.ssh/id_dbserver-test

sudo ulimit -c unlimited
sudo cd /vagrant
sudo sbt rpm:packageBin

SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
    config.vm.provision "shell", inline: $script
    config.vm.network "forwarded_port", guest: 9000, host: 9000
    # config.vm.synced_folder "./", "/home/vagrant/proyecto-gcs"
  end
end

