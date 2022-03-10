# how_to_install_pm2


////////
// node js
////////
```console
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.35.3/install.sh | bash
nvm list
nvm ls-remote
nvm install 14.18.3 <----------(20 jan 2022 LTS)
nvm use 14.18.3
nvm alias default 14.18.3
node -v
npm install -g npm
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```


////////
// pm2 
////////
```console
npm install pm2@4.5.6 -g
pm2 install pm2-logrotate
sudo env PATH=$PATH:/home/ubuntu/.nvm/versions/node/v14.18.3/bin /home/ubuntu/.nvm/versions/node/v14.18.3/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu
sudo systemctl enable pm2-ubuntu
```

////////
// optional for configure logrotate
////////
```console
pm2 set pm2-logrotate:compress true
pm2 set pm2-logrotate:max_size 1M
pm2 set pm2-logrotate:retain 10
```

//////////////////
// slice pm2.service
//////////////////
```console
sudo nano /etc/systemd/system/pm2-ubuntu.slice
```
```
[Slice]
Slice=pm2-ubuntu.slice
MemoryLimit=128M
CPUQuota=100%
```
```console
sudo nano /etc/systemd/system/pm2-ubuntu.service
```
```
Slice=pm2-ubuntu.slice
```
