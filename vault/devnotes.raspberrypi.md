---
id: lhba46lu14mpydc48injol4
title: Raspberrypi
desc: 'Raspberry Pi Setup Notes'
updated: 1647067092517
created: 1647065899204
---
## General Info

Getting the installation of Home Assistant and PiHole was a pain. This is not a good note.

Was easiest to do the install with Docker Compose, my router from AT&T does not accept custom DNS so I had to use the PiHole as a DHCP Server. Had to modify the docker compose file and add a couple environmental variables to make it work. Will document these tomorrow.
