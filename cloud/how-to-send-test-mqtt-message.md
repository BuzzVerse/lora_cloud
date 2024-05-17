# 📨 How to send test MQTT message

{% code fullWidth="false" %}
```bash
mosquitto_pub -h 192.169.1.1 -u admin -P pass -t 'tele/lora/SENSOR' -m '{"time": 1709226534260, "humidity":21, "temperature":37, "battery_voltage_mv":3000}' -d
```
{% endcode %}
