## Use 163 source
https://mirrors.163.com/.help/ubuntu.html

## Install docker in ubuntu
https://docker-practice.github.io/zh-cn/install/ubuntu.html

## Docker network for multiples container exchanging data
`sudo docker network create edgnite-iot`


## Ignite docker containers
- docker compose up  
`sudo docker compose up -d` 

- publish IoT data thru MQTT for testing  
`sudo docker container exec mosquitto mosquitto_pub -t 'edgnite/temperature' -m 'edgnite_temperature celsius=20 deviceId=lg-1'`  
`sudo docker container exec mosquitto mosquitto_pub -t 'edgnite/sensors' -m 'edgnite_power sensor_id=1,power=8 deviceId=lg-2'`

- grafana query with flux

http://localhost:8086/

```
from(bucket: "tsm_wx_data")
  |> range(start: v.timeRangeStart, stop: v.timeRangeStop)
  |> filter(fn: (r) => r["_measurement"] == "edgnite_temperature")
  |> aggregateWindow(every: v.windowPeriod, fn: mean, createEmpty: false)
  |> yield(name: "mean")
```


## Useful Command line
sudo docker stop $(sudo docker ps -a -q) 

sudo docker rm -v $(sudo docker ps -a -q)

sudo docker rmi $(sudo docker images -a -q)


sudo docker exec influxdb env

sudo docker logs influxdb
sudo docker volume ls
sudo docker volume rm volume_name volume_name


sudo docker volume rm docker_grafana-data docker_influxdb-config docker_influxdb-data 


sudo docker volume rm edgnite_grafana-data edgnite_influxdb-config edgnite_influxdb-data
