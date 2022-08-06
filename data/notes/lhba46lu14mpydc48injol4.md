## General Info

Getting the installation of Home Assistant and PiHole was a pain. This is not a good note.

Was easiest to do the install with Docker Compose, my router from AT&T does not accept custom DNS so I had to use the PiHole as a DHCP Server. Had to modify the docker compose file and add a couple environmental variables to make it work. Will document these tomorrow.

## Home Assistant Container Installation

```bash
docker run -d \
  --name homeassistant \
  --privileged \
  --restart=unless-stopped \
  -e TZ=America/Los_Angeles \
  -v /home/pi/homeassistant \
  --network=host \
  ghcr.io/home-assistant/home-assistant:stable
  ```

## Docker Commands

```bash
docker container ls
docker container rm $CONTAINER_NAME
docker image ls
docker image rm $IMAGE_ID
```

## General RPI Commands

```bash
sudo rfkill block wifi
sudo rfkill block bluetooth
sudo rfkill unblock wifi
```

## How to Reset DHCP Settings

```bash
sudo service dhcpcd status
sudo service dhcpcd start
sudo systemctl enable dhcpcd
sudo nano /etc/dhcpcd.conf
```
