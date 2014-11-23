tor-bw
======

The files needed to extend RPi-Monitor and show a Tor relay's bandwidth data.

## Introduction ##

[RPi-Monitor](http://rpi-experiences.blogspot.com.br/p/rpi-monitor.html) is a nice monitoring tool for your Raspberry Pi. It provides a web view where you can watch things such as memory, CPU and temperature. If your RPi is running a Tor relay then you can easily extend RPi-Monitor to show how much bandwidth the relay is taking.

![Stats](https://raw.githubusercontent.com/lzkill/tor-bw/master/stats.jpg)

## License ##

These files may be used under the terms of the MIT License, wich a [copy](LICENSE) is included in the download.

## Dependencies ##

- [Python](https://www.python.org) 2.6 or greater
- [Stem](https://stem.torproject.org) 1.2.2 or greater
- [Supervisor](http://supervisord.org)

## Usage ##

- Copy [tor.conf](tor.conf) to `/etc/rpimonitor/template/`
- Copy [tor.png](tor.png) to `/usr/share/rpimonitor/web/img`
- Copy [tor-bw.conf](tor-bw.conf) to `/etc/supervisor/conf.d/`
- Run `sudo groupadd supervisor;sudo usermod -a -G supervisor pi`
- Modify `/etc/supervisor/supervisord.conf` with the following:
```
[unix_http_server]
file=/var/run/supervisor.sock
chmod=0770
chown=root:supervisor
```
- Copy [tor-bw.py](tor-bw.py) to `/srv/`  
- Set your connection parameters on [tor-bw.py](tor-bw.py) (`TOR_CONTROL_PORT`, `TOR_ADDRESS` and `TOR_CONTROLLER_PASSWD`)
- Logout/login and run `sudo mkdir /usr/share/tor/statistics;sudo service supervisor restart;sudo service rpimonitor restart`

The statistical graph shows the values of `RelayBandwidthRate` and `RelayBandwidthBurst` if these parameters are set in `torrc`.

## Your Improvements ##

If you add improvements to these files please send them to me as pull requests on GitHub. I will add them to the next release so that everyone can enjoy your work. You might also benefit from it as others may fix bugs in your files or may continue to enhance them.

## Thanks ##

With regards from

[Luiz Kill](mailto:me@lzkill.com)

