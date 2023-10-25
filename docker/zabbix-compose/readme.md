## Запуск zabbix-compose

1. Установить docker + docker compose https://docs.docker.com/compose/install/
2. Скачать в локальный каталог /data/zabbix-docker/
https://github.com/zabbix/zabbix-docker/tree/6.4
3. Выбрать подходящий compose file ( docker-compose_v3_alpine_pgsql_latest.yaml )
4. Запустить из каталога 
```sudo docker compose -f docker-compose_v3_alpine_pgsql_latest.yaml up -d```
5. Проверить, что zabbix запускается на 80 порту
6. Проставить ```restart: always``` для сервисов
- `zabbix-docker-db_data_pgsql-1`
- `zabbix-docker-postgres-server-1`
- `zabbix-docker-zabbix-server-1`
- `zabbix-docker-zabbix-web-nginx-pgsql-1`