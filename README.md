# Nginx + Prometheus (Nginx Exporter + Nginxlog) + Grafana

### I. Запуск.
1. Скопировать `prometheus/prometheus.yml`, `nginxlog_exporter/nginxlog_exporter.yml`, `.env` и `docker-compose.yml` в рабочую директорию
2. Создать директории для данных Prometheus и Grafana:
<pre>mkdir prometheus/data
mkdir grafana/data</pre>
3. Изменить права:
<pre>
sudo chown 472:0 -Rc grafana/data
sudo chown -Rc 65534:65534 prometheus/data
</pre>
4. Настроить .env
   
Указать логин и пароль для доступа в Grafana в <i>GF_SECURITY_ADMIN</i>. 

5. Заменить сервис `nginx` в `docker-compose.yml`, а также минимальную конфигурацию nginx на используемую в проекте
6. Добавить в свою конфигурацию nginx новый формат логов и путь `/stub_status`
7. Запуск
<pre>
docker-compose up -d
</pre>

### II. После запуска.
1. Зайти в Grafana на localhost:3000 и добавить Data Source -> Prometheus. 
2. В качестве адреса `Prometheus server URL` использовать `http://prometheus:9090` 
3. Добавить панели. Как вариант:
    
   1) В Grafana: Меню -> Dashboards -> New -> Import
   2) Перетаскиваем `nginx-nginxlog-exporter.json` в окно `Upload dashboard JSON file` 

# Credits
- [rvva](https://github.com/rvva/nginx-prometheus-grafana), MIT license
