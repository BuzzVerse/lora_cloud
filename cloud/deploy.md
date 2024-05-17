---
description: How to deploy Grafana, InfluxDB, Mosquitto broker with docker image
---

# 🏗️ Deploy

1. Generate password for mosquitto broker

```bash
sudo apt-get install mosquitto-clients
mosquitto_passwd -c mosquitto.passwd admin
```

2. Set the password at:

{% code title="telegraf.conf" %}
```bash
[[inputs.mqtt_consumer]]
  username = "admin"
  password = "zaq1@WSX"
```
{% endcode %}

3. You can change password and API token for InfluxDB at:

{% code title="docker-compose.yml " %}
```bash
influxdb:
    environment:
      - DOCKER_INFLUXDB_INIT_MODE=setup
      - DOCKER_INFLUXDB_INIT_USERNAME=admin
      - DOCKER_INFLUXDB_INIT_PASSWORD=zaq1@WSX
      - DOCKER_INFLUXDB_INIT_ORG=bUZzverse
      - DOCKER_INFLUXDB_INIT_BUCKET=lora_db
      - DOCKER_INFLUXDB_INIT_ADMIN_TOKEN=gwTFtAnBRUM3OYmwsZ0GTg2C6r63bZ1G
```
{% endcode %}

If you change the token remember to set it at:

{% code title="grafana-provisioning/datasources/automatic.yml" %}
```bash
   secureJsonData:
      token: gwTFtAnBRUM3OYmwsZ0GTg2C6r63bZ1G
```
{% endcode %}

4. Run docker-compose

```bash
docker-compose up -d
```

5.  How to use\


    Go to http://localhost:3000/login \
    Login with `admin:admin` \
    Set new grafana admin password

    \
