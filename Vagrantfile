Vagrant.configure(2) do |config|

  config.vm.box = "centos/7"
  config.vm.network "forwarded_port", guest: 8081, host: 8081
  
  config.vm.provider "virtualbox" do |v|
    v.memory = 8192
  end

  config.vm.provision "shell", inline: "export START_TMO=240"

  config.vm.provision "shell", inline: "yum install java-1.8.0-openjdk-devel -y" 
  config.vm.provision "shell", inline: "yum install -y postgresql-server"
  config.vm.provision "shell", inline: "yum install -y wget unzip net-tools"
  config.vm.provision "shell", inline: "postgresql-setup initdb"
  config.vm.provision "shell", inline: "service postgresql start"
  config.vm.provision "shell", inline: "sudo su -c 'psql < /vagrant/scripts/db.sql' postgres"
  config.vm.provision "shell", inline: "wget https://bintray.com/jfrog/artifactory-pro-rpms/rpm -O bintray-artifactory-pro-rpms.repo"
  config.vm.provision "shell", inline: "mv bintray-artifactory-pro-rpms.repo /etc/yum.repos.d/"
  config.vm.provision "shell", inline: "yum install -y jfrog-artifactory-pro-5.10.4-51004900"
  config.vm.provision "shell", inline: "cp /vagrant/files/storage.properties /var/opt/jfrog/artifactory/etc/storage.properties"
  config.vm.provision "shell", inline: "wget https://jdbc.postgresql.org/download/postgresql-9.2-1004.jdbc41.jar"
  config.vm.provision "shell", inline: "mv postgresql-9.2-1004.jdbc41.jar /var/opt/jfrog/artifactory/tomcat/lib/"
  config.vm.provision "shell", inline: "service artifactory start"

end
