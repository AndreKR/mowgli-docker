# Mowgli in Docker

This container runs OpenMower Mowgli software remotely.

## Setup

### Mower PI

Be sure you don't run ROS along with ser2net in order to avoid conflicts

```bash
apt-get install -y ser2net
systemctl enable ser2net
```

Edit /etc/ser2net.conf and add theses lines on the bottom, change devices according to your setup

```
# Mowgli
4001:raw:600:/dev/ttyACM0:230400 8DATABITS NONE 1STOPBIT
# GPS
4002:raw:600:/dev/ttyACM1:230400 8DATABITS NONE 1STOPBIT
# IMU
4003:telnet:600:/dev/ttyAMA0:9600 8DATABITS NONE 1STOPBIT
```

Finally

```bash
systemctl start ser2net
```

### Remote Machine

- Clone this repository somewhere on your system.
- Install Docker ( curl -sSL https://get.docker.com | sh )
- Edit your Mowgli config in the config directory
- Put your map in the ros directory.

Finally, launch:

```bash
MOWER_IP=your_mower_ip docker-compose up
```

or, if you want to have it in deamon mode

```bash
MOWER_IP=your_mower_ip docker-compose up -d
```

That's it !

## Usage

### Buttons

You can use the scripts in buttons directory to press home / start

### Logs

```bash
docker-compose logs -f mowgli
```

### Shutdown

```bash
docker-compose stop
```