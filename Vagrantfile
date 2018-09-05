Vagrant.configure(2) do |config|

  config.vm.box = "centos/7"
  config.vm.network "forwarded_port", guest: 8081, host: 8081
  
  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
  end

  config.vm.provision "shell", inline: "yum install java-1.8.0-openjdk-devel -y" 
  config.vm.provision "shell", inline: "yum install -y postgresql-server"
  config.vm.provision "shell", inline: "yum install -y wget unzip net-tools"
  config.vm.provision "shell", inline: "sudo postgresql-setup initdb"
  config.vm.provision "shell", inline: "sudo service postgresql start"
  config.vm.provision "shell", inline: "sudo su -c 'psql < /vagrant/scripts/db.sql' postgres"
  config.vm.provision "shell", inline: "wget https://bintray.com/jfrog/artifactory-pro/download_file?file_path=org%2Fartifactory%2Fpro%2Fjfrog-artifactory-pro%2F5.10.4%2Fjfrog-artifactory-pro-5.10.4.zip"
  config.vm.provision "shell", inline: "unzip download_file\?file_path\=org%2Fartifactory%2Fpro%2Fjfrog-artifactory-pro%2F5.10.4%2Fjfrog-artifactory-pro-5.10.4.zip -d /opt/"
  config.vm.provision "shell", inline: "cp /vagrant/files/storage.properties /opt/artifactory-pro-5.10.4/etc/storage.properties"
  config.vm.provision "shell", inline: "wget https://jdbc.postgresql.org/download/postgresql-9.2-1004.jdbc41.jar"
  config.vm.provision "shell", inline: "cp postgresql-9.2-1004.jdbc41.jar /opt/artifactory-pro-5.10.4/tomcat/lib/"
  config.vm.provision "shell", inline: "/opt/artifactory-pro-5.10.4/bin/installService.sh"
  config.vm.provision "shell", inline: "service artifactory start"

end
