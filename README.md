## Установка локального мониторинга
Grafana + prometheus + node_exporter

запуск:  docker compose up -d

http://IP:3000

в Grafana добавить datasource -> prometheus: http://prometheus:9090
импортировать dashboard 1860  (https://grafana.com/grafana/dashboards/1860-node-exporter-full/)
