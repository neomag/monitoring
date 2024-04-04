## Установка локального мониторинга
Grafana + prometheus + node_exporter

запуск:  
docker compose up -d  
chown nobody -R ./prometheus-vol 


http://IP:3000
admin/admin

в Grafana добавить datasource -> Prometheus -> server URL -> http://prometheus:9090  
импортировать dashboard 1860  (https://grafana.com/grafana/dashboards/1860-node-exporter-full/)  


после запуска будут открыты порты  3000, 9090, 9100  
в случае потребности закрыть доступ с внешних сетей или пр налчиии firewall стоит учитывать следующее:  
порт 9100: закрывается в цепочке INPUT потому что используется тип сети network_mode: host  
порт 9090: iptables -I DOCKER-USER -p tcp --dport 9090 -j DROP  
порт 3000: iptables -I DOCKER-USER -p tcp --dport 3000 -j DROP  
пропуск трафика с bridge контейнеров на host(node exporter):
iptables -A DOCKER-USER -s 172.33.0.0/24 -j ACCEPT  

подробнее об особенностях использования iptables и docker:  
https://docs.docker.com/network/packet-filtering-firewalls/  