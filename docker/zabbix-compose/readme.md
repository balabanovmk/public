## Запуск zabbix-compose

1. Установить docker + docker compose https://docs.docker.com/compose/install/
2. Скачать в локальный каталог /data/zabbix-docker/
https://github.com/zabbix/zabbix-docker/tree/6.4
3. Выбрать подходящий compose file ( docker-compose_v3_alpine_pgsql_latest.yaml )
4. Запустить из каталога 
```sudo docker compose -f docker-compose_v3_alpine_pgsql_latest.yaml up -d```
5. Проверить, что zabbix запускается на 80 порту
6. Создать unit-file для запуска как службы
```/etc/systemd/system/zabbix-compose.service
[Unit]
Description=Zabbix services with docker-compose
Requires=docker.service
After=docker.service

[Service]
WorkingDirectory=/data/zabbix-docker/
User=root
Type=oneshot
RemainAfterExit=yes

ExecStartPre=/usr/local/bin/docker-compose -f /data/zabbix-docker/docker-compose_v3_alpine_pgsql_latest.yaml -v

# Compose up
ExecStart=/usr/local/bin/docker-compose -f /data/zabbix-docker/docker-compose_v3_alpine_pgsql_latest.yaml up -d

# Compose down, remove containers
ExecStop=/usr/local/bin/docker-compose -f /data/zabbix-docker/docker-compose_v3_alpine_pgsql_latest.yaml down

[Install]
WantedBy=multi-user.target
```
7. Автозапуск сервиса ```sudo systemctl enable zabbix-compose.service```