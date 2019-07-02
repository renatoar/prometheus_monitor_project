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

## Acesso as aplicações

 - Prometheus: http://192.168.50.10:9090
 - TransferFile: http://192.168.50.20:8000/
 - Grafana: http://192.168.50.10:3000/
 - VM Monitor e Containers Monitor: Instalar solução para conexão com banco e visualização de dados (Sugerido Robo 3T) e fazer conexão em http://192.168.50.20:17017/

## Instalação Windows

 - Instalar Vagrant.
 - Instalar VirtualBox.
 - Rodar comando 'vagrant up' na pasta do projeto.
Para acessar as máquinas o comando é o mesmo: 'vagrant ssh nome_da_vm'

## Repositórios das aplicações usadas no projeto:
    
- Prometheus para monitoramento: https://github.com/renatoar/prometheus_monitoring_docker.git
- App Monitor de Container: https://github.com/renatoar/monitoring_container.git
- App Monitor de VMs (Hosts): https://github.com/renatoar/vm_monitoring_container.git
- App Transferência de arquivos: https://github.com/renatoar/transferfileapp_container.git

## Dificuldades de implementação

Uma das dificuldades encontradas foi descobrir por que os containers das aplicações de persistência de dados monitorados caíam depois de alguns segundos. Depois de muitos testes, descobrimos que havia erros na aplicação python que por consequência derrubava os containers.

Também vale citar que a aplicação de transfência de arquivos não está totalmente implementada por termos focado mais tempo nos outros aspectos do projeto. No estado atual ela apenas expôe os diretórios raiz do container, ou seja, é possível replicar testes de transferência e não de recebimento de arquivos. Essa aplicação é um recurso básico do python que cria um servidor para testes.
