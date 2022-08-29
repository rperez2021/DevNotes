---
id: 3fs913dkj8phwyo1k6yvloc
title: Mqtt
desc: ''
updated: 1661619961485
created: 1661616401615
---
## General Information

MQTT is a lightweight pub/sub machine to machine network protocol. It is designed for connections with remote locations that have devices with resource constraints or limited network bandwidth. It must run over a transport protocol that provides ordered, lossless, bi-directional connections—typically, TCP/IP. It is an open OASIS standard and an ISO recommendation (ISO/IEC 20922).

## Documentation

[All Mosquitto Man Pages](https://mosquitto.org/documentation/)

## Commands

### To Publish a Message

`mosquitto_pub -d -t testTopic -m "Hello world!" -u <USERNAME> -P <PASSWORD>`

### To Subscribe to a Message from another Device

`mosquitto_sub -d -t testTopic -h <HOSTNAME or IP> -u <USERNAME> -P <PASSWORD>`

### To Restart Mosquitto 

`sudo service mosquitto restart`