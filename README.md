# Monitorando containers Docker com Prometheus

Trabalho prático da disciplina de Tópicos Avançados em Redes de Computadores e Sistemas Distribuidos. UFScar Sorocaba

# Como usar (Se for montar as VMs localmente, ir para o passo 4)

1-Executar o comando abaixo e acessar pasta /slice-enablers/arquivos
	https://github.com/dcomp-leris/slice-enablers.git

2-Usar os comandos abaixo para acessar cloud ufscar
```
	chmod 400 arquivos/cloud_ufscar_rsa.dms
	ssh -i cloud_ufscar_rsa.dms ubuntu@200.136.252.136
```
3-Já na cloud ufscar (ubuntu@master) acessar pasta abaixo e acessar VM do grupo 2
```
	cd slice-enablers/arquivos
	sh acessar.sh 2
```
4-Baixar o projeto pelo comando abaixo e acessar pasta 
```	
    git clone https://github.com/renatoar/prometheus_monitor_project.git
	cd prometheus_monitor_project
```

5-Subir as máquinas virtuais já com as aplicações configuradas pelo comando abaixo: 
```	
    vagrant up
```

Testes:
