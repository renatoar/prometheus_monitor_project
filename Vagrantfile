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
			git clone https://github.com/renatoar/prometheus_monitoring_docker.git
			cd prometheus_monitoring_docker
			sudo docker build -t prometheus_monitor .
			sudo docker run -p 9090:9090 --restart=always --detach=true --name=prometheus prometheus_monitor
			sudo docker run -d --restart=always --net="host" --pid="host" --publish=9100:9100 --detach=true --name=node-exporter -v "/:/host:ro,rslave" quay.io/prometheus/node-exporter --path.rootfs /host
			sudo docker run --restart=always --volume=/:/rootfs:ro --volume=/var/run:/var/run:ro --volume=/sys:/sys:ro --volume=/var/lib/docker/:/var/lib/docker:ro --volume=/dev/disk/:/dev/disk:ro --publish=8080:8080 --detach=true --name=cadvisor google/cadvisor:latest
			sudo docker run -d --name=grafana -p 3000:3000 grafana/grafana
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
			sudo docker run -d --restart=always --net="host" --pid="host" --publish=9100:9100 --detach=true --name=node-exporter -v "/:/host:ro,rslave" quay.io/prometheus/node-exporter --path.rootfs /host
			sudo docker run --restart=always --volume=/:/rootfs:ro --volume=/var/run:/var/run:ro --volume=/sys:/sys:ro --volume=/var/lib/docker/:/var/lib/docker:ro --volume=/dev/disk/:/dev/disk:ro --publish=8080:8080 --detach=true --name=cadvisor google/cadvisor:latest
			sudo docker run --name mongodb -p 17017:27017 -d mongo
			git clone https://github.com/renatoar/monitoring_container.git
			git clone https://github.com/renatoar/vm_monitoring_container.git
			git clone https://github.com/renatoar/transferfileapp_container.git
			#cd monitoring_container
			#sudo docker build -t containers_monitor .
			#sudo docker run -d --name containers_monitor containers_monitor
			#cd vm_monitoring_container
			#sudo docker build -t vm_monitor .
			#sudo docker run -d --name vm_monitor vm_monitor
			#cd transferfileapp_container
			#sudo docker build -t transferfileapp .
			#sudo docker run -d -p 8000:8000 --name transferfileapp transferfileapp
		SHELL
	end
end
