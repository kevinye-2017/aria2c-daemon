# aria2c-daemon
two file
1. /etc/aria2.daemon 

continue
daemon=true
dir=/home/aria2/Downloads
file-allocation=falloc
log-level=warn
max-connection-per-server=4
max-concurrent-downloads=3
max-overall-download-limit=0
min-split-size=5M
enable-http-pipelining=true

enable-rpc=true
rpc-listen-all=true

2. /usr/lib/systemd/system/aria2.service 
[Unit]
Description=Aria2c download manager
Requires=network.target
After=dhcpcd.service
   
[Service]
Type=forking
User=root
RemainAfterExit=yes
ExecStart=/usr/bin/aria2c --conf-path=/etc/aria2.daemon
ExecReload=/usr/bin/kill -HUP $MAINPID
RestartSec=1min
Restart=on-failure
   
[Install]
WantedBy=multi-user.target


systemctl enable aria2  

systemctl start aria2
