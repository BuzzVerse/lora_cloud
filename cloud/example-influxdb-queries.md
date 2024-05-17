# 💬 Example InfluxDB queries

1. Display temperature in Grafana

```bash
from(bucket: "lora_db")
  |> range(start: v.timeRangeStart, stop: v.timeRangeStop)
  |> filter(fn: (r) => r._field == "temperature" and r._measurement == "SENSOR_NAME")
  |> last()
```
