# Monitorando containers Docker com Prometheus

Trabalho prático da disciplina de Tópicos Avançados em Redes de Computadores e Sistemas Distribuidos. UFScar Sorocaba

![Overview Image](https://user-images.githubusercontent.com/18008072/60396845-d10a1800-9b1c-11e9-80e4-16f5fdf170e7.jpg)


## Como usar (Se for montar as VMs localmente, ir para o passo 4)

1 - Executar o comando abaixo e acessar pasta /slice-enablers/arquivos
	https://github.com/dcomp-leris/slice-enablers.git

2 - Usar os comandos abaixo para acessar cloud ufscar
```
	chmod 400 arquivos/cloud_ufscar_rsa.dms
	ssh -i cloud_ufscar_rsa.dms ubuntu@200.136.252.136
```
3 - Já na cloud ufscar (ubuntu@master) acessar pasta abaixo e acessar VM do grupo 2
```
	cd slice-enablers/arquivos
	sh acessar.sh 2
```
4 - Baixar o projeto pelo comando abaixo e acessar pasta 
```	
    git clone https://github.com/renatoar/prometheus_monitor_project.git
	cd prometheus_monitor_project
```

5 - Subir as máquinas virtuais pelo comando abaixo: 
```	
    vagrant up
```

6 - Após termino da configuração do Vagrant, acessar a vmworker pelo comando abaixo:
```	
    vagrant ssh vmworker
```

7 - Procurar e copiar do terminal o comando 'docker swarm join' e rodar na máquina vmworker.


8 - Rodar os comandos abaixo para subir as imagens dos containers e coloca-los em funcionamento
```	
    # App Monitor de Container
    cd monitoring_container
    sudo docker build -t containers_monitor .
    sudo docker run -d --name containers_monitor containers_monitor
    # App Monitor de VMs (Hosts)
    cd vm_monitoring_container
    sudo docker build -t vm_monitor .
    sudo docker run -d --name vm_monitor vm_monitor
    # App Transferência de arquivos
    cd transferfileapp_container
    sudo docker build -t transferfileapp .
    sudo docker run -d -p 8000:8000 --name transferfileapp transferfileapp
```

## Instalação Windows

 - Instalar Vagrant.
 - Instalar VirtualBox.
 - Rodar comando 'vagrant up' na pasta do projeto.
 - Para acessar as máquinas o comando é o mesmo 'vagrant ssh nome_da_vm'

## Repositórios das aplicações usadas no projeto:
    ```
    - Prometheus para monitoramento

        git clone https://github.com/renatoar/prometheus_monitoring_docker.git

    - App Monitor de Container

        git clone https://github.com/renatoar/monitoring_container.git

    - App Monitor de VMs (Hosts)

        git clone https://github.com/renatoar/vm_monitoring_container.git

    - App Transferência de arquivos

        git clone https://github.com/renatoar/transferfileapp_container.git
    ```