PROJECT="auth"

#Targets principales
install: vagrantup

down: composedown vagrantdelete

delete: composedelete vagrantdelete

start: vagrantstart

stop: vagrantstop

restart: stop start

sh:
	docker compose -p ${PROJECT} -f compose/docker-compose.yml exec ${service} bash

info:
	docker inspect ${PROJECT}_${service}_1

ls:
	docker compose -p ${PROJECT} -f compose/docker-compose.yml ps

#Requisitos
vagrantup: composeup
	sed -i "s/<ipvlan_bridge>/di-$(shell docker network ls | grep auth_radius | cut -d' ' -f1)/" vagrant/Vagrantfile
	cd vagrant && vagrant up
composeup:	
	docker compose -p ${PROJECT} -f compose/docker-compose.yml up -d
	-xhost si:localuser:root
	
vagrantdelete:
	cd vagrant && vagrant destroy -f
composedelete:
	sed -i "s/<ipvlan_bridge>/di-$(shell docker network ls | grep auth_radius | cut -d' ' -f1)/" vagrant/Vagrantfile
	docker compose -p ${PROJECT} -f compose/docker-compose.yml down --rmi all -v

composedown:
	sed -i "s/<ipvlan_bridge>/di-$(shell docker network ls | grep auth_radius | cut -d' ' -f1)/" vagrant/Vagrantfile
	docker compose -p ${PROJECT} -f compose/docker-compose.yml down

vagrantstart: composestart
	cd vagrant && vagrant up
composestart:
	docker compose -p ${PROJECT} -f compose/docker-compose.yml start
	-xhost si:localuser:root	

vagrantstop: composestop
	cd vagrant && vagrant halt
composestop:
	docker compose -p ${PROJECT} -f compose/docker-compose.yml stop


