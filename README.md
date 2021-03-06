# Workshop 2

## Goal:
* Intro to docker-compose
* Lab 1: Automate with docker-compose: container mqtt_broker + container dsmr_sim
* Intro Openhab
* Intro Influxdb + "Downsampling + Dataretention policies"
* Lab 2: Build the final openmeter solution with docker-compose

## 1. Docker-compose

Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a **YAML** file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration.

```bash
# to start your multi-container application
docker-compose up

# to stop it:
docker-compose down
```
### What is the difference between docker-compose and Swarm?

**They are very similar but:**

* docker-compose -> works on single host -> typical for DevOps or developers
* Swarm     -> works over multiple hosts

<img src="./img/RPI_Swarm_Stack.png" alt="Swarm Stack" width="400px">

## 2. Lab 1: mqtt_broker + dsmr_sim

```bash
#
ssh pi@192.168.2.151

# Get the repository
sudo git clone https://github.com/openmeter/openmeter.git

# eliminate read/write conflict between user space in container vs shared drive on RPI
chmod 777 -R openmeter

cd openmeter

#execute docker-compose
# default = docker-compose up -d
# Now we dont't want the default file (docker-compose.yaml) but test.yaml -> specified with '-f'
docker-compose -f test.yaml up -d
```
### Check:
* running containers        ->         'docker ps'
* networks                  ->         'docker network inspect backend
* individual container      ->          'docker inspect mqtt_broker'
* if it works with MQTT-Explorer

### In case of problems
* look if container run     ->          'docker ps' will return 'restarting or exited'
* look at logs              ->          'docker logs mqtt_broker'

### Bring your infrastructure down

```bash
docker-compose -f test.yaml down
```

## 3. Intro Openhab

Look at:
* [this repo](https://github.com/tribp/DSMR-Fluvius-MQTT-Openhab)
* BK Hobby at youtube

## 4. Intro Influxdb

[openmeter Influxdb](https://github.com/openmeter/openmeter/blob/master/INFLUXDB.md)

## 5. Lab 2:

```bash
# Build working solution with a simulated Smartmeter
docker-compose up -d
```

### Check:

* if mqtt_broker works with MQTT-Explorer
* Check openhab
    * http://yourRPIipAddress:8080
* Check Influxdb
    * docker exec -it influxdb bash
        * run the queries or other commands
* Configure and connect with your mobile app

## 6. Lab 3:

Build a solution with real smartmeter

## 7. Improve

### Create and suggest improvements by submitting 'issues' at openmeter

Suggestions:
* openhab workshop
* grafana configuration
* Business and product improvement 
