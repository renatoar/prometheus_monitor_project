# Monitorando containers Docker com Prometheus

Trabalho prático da disciplina de Tópicos Avançados em Redes de Computadores e Sistemas Distribuidos. UFScar Sorocaba

![Overview Image](https://user-images.githubusercontent.com/18008072/60402432-f8d19e00-9b65-11e9-8d67-827aba1fcedf.jpg)


## Como usar (Se for montar as VMs localmente, ir para o passo 4)

1 - Executar o comando abaixo e acessar pasta /slice-enablers/arquivos
```
	https://github.com/dcomp-leris/slice-enablers.git
```
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

## Estrutura de monitoramento

 - Prometheus: http://192.168.50.10:9090
 - TransferFile: http://192.168.50.20:8000/
 - Grafana: http://192.168.50.10:3000/

## Instalação Windows

 - Instalar Vagrant.
 - Instalar VirtualBox.
 - Rodar comando 'vagrant up' na pasta do projeto.
Para acessar as máquinas o comando é o mesmo: 'vagrant ssh nome_da_vm'

## Aplicação de transferência de arquivos

Este container expôe seus arquivos para acesso em http://192.168.50.20:8000

## Repositórios das aplicações usadas no projeto:
    
- Prometheus para monitoramento: https://github.com/renatoar/prometheus_monitoring_docker.git
- App Monitor de Container: https://github.com/renatoar/monitoring_container.git
- App Monitor de VMs (Hosts): https://github.com/renatoar/vm_monitoring_container.git
- App Transferência de arquivos: https://github.com/renatoar/transferfileapp_container.git