# ords-daemon
A simple systemd unit file to start and stop Oracle REST Data Services via systemctl
To create the unit file:
- login as root
- cd to /etc/systemd/system
- vi ords.service
- copy and paste the following file
- adapt the paths to your environment setup

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

To enable the service run the following commands:
- systemctl daemon-reload
- systemctl enable ords
- systemctl start ords

To check the service status run the following command:
 - systemctl status ords
