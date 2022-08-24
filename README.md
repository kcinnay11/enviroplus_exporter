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
cd
git clone https://github.com/tijmenvandenbrink/enviroplus_exporter.git
sudo cp -r enviroplus_exporter /usr/src/
sudo chown -R pi:pi /usr/src/enviroplus_exporter
```

2.Install dependencies for enviroplus-exporter
```sh
pip3 install -r requirements.txt
```

3.Install as a Systemd service
```sh
cd /usr/src/enviroplus_exporter
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
pi@raspberrypi:/usr/src/enviroplus_exporter $ sudo systemctl status enviroplus-exporter
● enviroplus-exporter.service - Enviroplus-exporter service
   Loaded: loaded (/etc/systemd/system/enviroplus-exporter.service; disabled; vendor preset: enabled)
   Active: active (running) since Fri 2020-01-17 14:13:41 CET; 5s ago
 Main PID: 30373 (python)
    Tasks: 2 (limit: 4915)
   Memory: 6.0M
   CGroup: /system.slice/enviroplus-exporter.service
           └─30373 /usr/bin/python /usr/src/enviroplus_exporter/enviroplus_exporter.py --bind=0.0.0.0 --port=8000

Jan 17 14:13:41 wall-e systemd[1]: Started Enviroplus-exporter service.
Jan 17 14:13:41 wall-e python[30373]: 2020-01-17 14:13:41.565 INFO     enviroplus_exporter.py - Expose readings from the Enviro+ sensor by Pimoroni in Prometheus format
Jan 17 14:13:41 wall-e python[30373]: Press Ctrl+C to exit!
Jan 17 14:13:41 wall-e python[30373]: 2020-01-17 14:13:41.581 INFO     Listening on http://0.0.0.0:8000
```

6.Enable at boot time
```sh
sudo systemctl enable enviroplus-exporter
```

## Enviro users

If you are using an Enviro (not Enviro+) add `--enviro=true` to the command line (in the `/etc/systemd/system/enviroplus-exporter.service` file) then it won't try to use the missing sensors.
