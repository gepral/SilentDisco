# SilentDisco

# Material
- Domestic Router
- Raspberry Pi 5
- Micro SD
- Laptop
- USB Audio Interface ( Used an old Audio 6 from Native Instruments )
- Wifi Access Point (If desired)
- Some Ethernet Cables 

# Objects Diagram

```mermaid
flowchart TB
    SoundInput[fas:fa-music Sound Input ]
    AudioInterface(far:fa-file-audio Audio Interface)
    Laptop[fas:fa-laptop Laptop]
    Server("fab:fa-raspberry-pi Server"
    192.168.1.2)
    Router["fas:fa-network-wired Router
    192.168.1.1"]
    UAP1["fas:fa-tower-broadcast UAP 1
    192.168.1.3"]
    UAP2["fas:fa-tower-broadcast UAP 2
    192.168.1.4"]
    U1[fas:fa-user 1]
    U2[fas:fa-user N]
    U3[fas:fa-user N + 1]
    USB[fab:fa-usb USB]


    subgraph Users
    direction TB
    U1-.-U2
    U2-.-U3
    end

    subgraph Network Map
    Laptop-.-BUTT_Software-..-Server
    SoundStream-.- USB -.-> Laptop
    Router<==>Server
    Laptop-->Router
    Router--->UAP1-.->Users
    Router--->UAP2-.->Users

Antenas-.-Users

    subgraph SoundStream
    direction TB
    SoundInput -- "ADC" --> AudioInterface
    end

    subgraph Antenas
    UAP1
    UAP2 
    end
    end

    
```

# Software 
To be installed on the computer:
- Ubuntu imager for Raspberry: (https://ubuntu.com/download/raspberry-pi)
- Butt Broadcast tool: (https://danielnoethen.de/butt/)


# Server Preparation (Raspberry or WSL)
1. Start server and put up to date all packages

```shell
$  sudo apt update
$  sudo apt upgrade
$  sudo reboot
```

2. Install all needed apps for the project
   - When installing IceCast2 you can press enter on default configurations or put your own password for each user

```shell
$  sudo apt install icecast2
$  sudo apt install atop
```

3. Enable the icecast server to start at server boot

```shell
$  sudo systemctl enable icecast2
$  sudo systemctl start icecast2
```
4. Validate that icecast is running fine with one of this 2 commands

```shell
$  ps -aux | grep icecast
$  systemctl status icecast2
```

5. Next (optional), Changing the Logs folder to be inside the icecast installation and config folder

```shell
$  cd /etc/icecast2
$  sudo mkdir logs
$  sudo chmod 777 logs
```

6. Edit finally the logs destination folder just created on the config file

```shell
$  sudo nano /etc/icecast2/icecast.xml
```
Then change on the file the <logdir> content by the following one

```xml
<logdir>/etc/icecast2/logs</logdir>
```


7. 








