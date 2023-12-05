<p align="center">
  <img width="726" alt="image" src="https://github.com/BuzzVerse/lora_cloud/assets/19632192/f8764074-3613-497b-b8a7-68bacd0e89ec">
</p>


## How to deploy
1. Generate password for mosquitto broker
```bash
sudo apt-get install mosquitto-clients
mosquitto_passwd -c mosquitto.passwd admin
```

2. Set the password in telegraf.conf at:
```bash
[[inputs.mqtt_consumer]]
  username = "admin"
  password = "qwerty"
```

3. You can change password and API token for InfluxDB in docker-compose.yml at:
```bash
  influxdb:
    ...
    environment:
      - DOCKER_INFLUXDB_INIT_MODE=setup
      - DOCKER_INFLUXDB_INIT_USERNAME=admin
      - DOCKER_INFLUXDB_INIT_PASSWORD=zaq1@WSX
      - DOCKER_INFLUXDB_INIT_ORG=bUZzverse
      - DOCKER_INFLUXDB_INIT_BUCKET=lora_db
      - DOCKER_INFLUXDB_INIT_ADMIN_TOKEN=gwTFtAnBRUM3OYmwsZ0GTg2C6r63bZ1G
```
If you change the token remember to set it in grafana-provisioning/datasources/automatic.yml at:
```bash
    secureJsonData:
      token: gwTFtAnBRUM3OYmwsZ0GTg2C6r63bZ1G
```

4. Run docker-compose
```bash
docker-compose up -d
```

## How to use
1. Go to http://localhost:3000/login
2. Login with admin:admin
3. Set new grafana admin password

## How to send test MQTT message
```bash
mosquitto_pub -u admin -P [pass_from_1_step] -t 'tele/lora/SENSOR' -m '{"humidity":21, "temperature":37, "battery_voltage_mv":3000}' -d
```

## example influx query to display temperature in Grafana
```bash
from(bucket: "lora_db")
|> range(start: v.timeRangeStart, stop:v.timeRangeStop)
|> filter(fn: (r) => r._field == "temperature")
```
