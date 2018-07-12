# ords-daemon
A simple systemd unit file to start and stop Oracle REST Data Services via systemctl

This is the sample file:
```
[Unit]
Description=Oracle REST Data Services
Requires=network.target
After=oracle-rdbms.service

[Service]
Type=simple
ExecStart=/bin/java -jar /opt/ords/ords.war
ExecStop=/bin/kill -HUP ${MAINPID}
User=oracle

[Install]
WantedBy=multi-user.target
```

Please change the value of the following parameters to meet your setup:
- **After**: Specify the Unit after which this one should be executed (I choose to run it after starting the Oracle Database)
- **ExecStart**: Adapt the directory of the ords.war file according to your ORDS installation (In this case /opt/ords)
