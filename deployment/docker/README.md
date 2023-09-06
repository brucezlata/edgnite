## Docker network for multiples container exchanging data
`docker network create edgnite-iot`

## Ignite docker containers
- docker compose up  
`docker-compose up -d` 

- publish IoT data thru MQTT
```
docker container exec mosquitto mosquitto_pub \
-t 'edgnite/temperature' \
-m 'edgnite_temperature celsius=20'
```

