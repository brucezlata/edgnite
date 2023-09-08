## Docker network for multiples container exchanging data
`docker network create edgnite-iot`

## Init secrets for influx db
```
echo fill_your_password > influx_user_password.txt
echo fill_your_token > influx_token.txt
```
## Ignite docker containers
- docker compose up  
`docker-compose up -d` 

- publish IoT data thru MQTT for testing  
`docker container exec mosquitto mosquitto_pub -t 'edgnite/temperature' -m 'edgnite_temperature celsius=20'`  
`docker container exec mosquitto mosquitto_pub -t 'edgnite/sensors' -m 'edgnite_power sensor_id=1,power=8'`

- grafana query with flux
```
from(bucket: "edgnite_iot_data")
  |> range(start: v.timeRangeStart, stop: v.timeRangeStop)
  |> filter(fn: (r) => r["_measurement"] == "edgnite_temperature")
  |> aggregateWindow(every: v.windowPeriod, fn: mean, createEmpty: false)
  |> yield(name: "mean")
```

