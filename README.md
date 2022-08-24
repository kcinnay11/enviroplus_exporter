<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://github.com/tijmenvandenbrink/enviroplus_exporter">
    <img src="logo/logo.png" alt="Logo" width="160" height="160">
  </a>

  <h3 align="center">Enviroplus-exporter</h3>
  
<!-- GETTING STARTED -->

### Prerequisites

- Python3
- To run the enviroplus-exporter you need to have the enviroplus-python library by Pimoroni installed:
 
### One-line (Installs enviroplus-python library from GitHub)

```sh
curl -sSL https://get.pimoroni.com/enviroplus | bash
```

**Note** Raspbian Lite users may first need to install git: `sudo apt install git`

### Installation
We're going to run the enviroplus-exporter as the user ```pi``` in the directory ```/usr/src/```. Adjust this as you wish.
 
1.Clone the enviroplus-exporter repository
```sh
cd /home/pi
git clone https://github.com/kcinnay11/enviroplus_exporter.git
sudo chown -R pi:pi /home/pi/enviroplus_exporter
```

2.Install dependencies for enviroplus-exporter
```sh
pip3 install -r requirements.txt
```

3.Install as a Systemd service
```sh
cd /home/pi/enviroplus_exporter
sudo cp contrib/enviroplus-exporter.service /etc/systemd/system/enviroplus-exporter.service
sudo chmod 644 /etc/systemd/system/enviroplus-exporter.service
sudo systemctl daemon-reload
```
4.Start the enviroplus-exporter service
```sh
sudo systemctl start enviroplus-exporter
```
5.Check the status of the service
```sh
sudo systemctl status enviroplus-exporter
```
If the service is running correctly, the output should resemble the following:

```
pi@enviroplus:~ $ sudo systemctl status enviroplus-exporter
● enviroplus-exporter.service - Enviroplus-exporter service
     Loaded: loaded (/etc/systemd/system/enviroplus-exporter.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2022-08-24 15:05:54 CEST; 1h 50min ago
   Main PID: 788 (python3)
      Tasks: 3 (limit: 191)
        CPU: 39.378s
     CGroup: /system.slice/enviroplus-exporter.service
             └─788 python3 /home/pi/enviroplus_exporter/enviroplus_exporter.py --bind=0.0.0.0 --port=8000 --influxdb=true --factor=2.4
```

6.Enable at boot time
```sh
sudo systemctl enable enviroplus-exporter
```

## Enviro users

If you are using an Enviro (not Enviro+) add `--enviro=true` to the command line (in the `/etc/systemd/system/enviroplus-exporter.service` file) then it won't try to use the missing sensors.
