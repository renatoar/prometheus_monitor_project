Vagrant.configure("2") do |config|
  config.vm.define "vmmaster" do |vmmaster|

 	vmmaster.vm.box = "ubuntu/bionic64"
 	vmmaster.vm.network "forwarded_port", guest: 9000, host: 9001
  	vmmaster.vm.network "private_network", ip: "192.168.50.10"
	vmmaster.vm.hostname = "vmmaster"
  	vmmaster.vm.provider "virtualbox" do |vb|
      		vb.memory = "1024"
    	  	vb.name = "vmmaster"
  	end
	vmmaster.vm.provision "shell", inline: <<-SHELL
		sudo apt update
		sudo apt -y upgrade
		wget -qO- https://get.docker.com/ | sh
		sudo apt update
		sudo apt -y install docker-ce docker-ce-cli containerd.io
		sudo systemctl start docker
		sudo systemctl enable docker
        sudo docker swarm init --advertise-addr 192.168.50.10:2377
        git clone 


		git clone https://github.com/RenatoAr/docker-appserver.git
		cd docker-appserver
		sudo docker build -t docker-appserver .
		sudo docker run -d -p 5000:5000 --name docker-appserver docker-appserver
	SHELL
  end
  config.vm.define "vmworker" do |vmworker|

 	vmworker.vm.box = "ubuntu/bionic64"
  	vmworker.vm.network "private_network", ip: "192.168.50.20"
	vmworker.vm.hostname = "vmworker"
  	vmworker.vm.provider "virtualbox" do |vb|
      		vb.memory = "512"
    	  	vb.name = "vmworker"
  	end
	vmworker.vm.provision "shell", inline: <<-SHELL
		sudo apt update
		sudo apt -y upgrade
		wget -qO- https://get.docker.com/ | sh
		sudo apt update
		sudo apt -y install docker-ce docker-ce-cli containerd.io
		sudo systemctl start docker
		sudo systemctl enable docker
		git clone https://github.com/RenatoAr/docker-appclient.git
		cd docker-appclient
		sudo docker build -t docker-appclient .
		sudo docker run -d -p 5000:5000 -v /var/run/docker.sock:/var/run/docker.sock --name docker-appclient docker-appclient
	SHELL
  end
end
