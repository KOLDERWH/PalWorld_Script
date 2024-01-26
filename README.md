## centos
### instll
```linux
yum -y install dnf &&dnf update -y && dnf install glibc.i686 libstdc++.i686  libcurl.i686 -y && dnf install ncurses-libs.i686 -y && dnf install screen vim wget -y && useradd -m steam && su steam -c ' cd && wget https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz &&tar -zxvf steamcmd_linux.tar.gz && ./steamcmd.sh +login anonymous +app_update 2394010 validate +quit&& mkdir -p ~/.steam/sdk64/ &&./steamcmd.sh +login anonymous +app_update 1007 +quit &&cp ~/Steam/steamapps/common/Steamworks\ SDK\ Redist/linux64/steamclient.so ~/.steam/sdk64/ '&&screen -dmS pal&&  screen -S pal -X stuff "su - steam$(printf \\r)" && screen -S pal -X stuff "cd && cd Steam/steamapps/common/PalServer/ && ./PalServer.sh -useperfthreads -NoAsyncLoadingThread -UseMultithreadForDS $(printf \\r)"&&screen -r pal
```

after that , you can press ctrl+d to siwtch to root.

### restart

```linux
 #!/bin/bash

pkill screen

screen -dmS pal
screen -S pal -X stuff "su - steam$(printf \\r)"

screen -S pal -X stuff "cd && cd Steam/steamapps/common/PalServer/ && ./PalServer.sh -useperfthreads -NoAsyncLoadingThread -UseMultithreadForDS $(printf \\r)"
```

### backup

```linux
#!/bin/bash
su steam -c '
if [ ! -d "/home/steam/Steam/steamapps/common/PalServer/Pal/backup" ]; then
  mkdir "/home/steam/Steam/steamapps/common/PalServer/Pal/backup"
fi &&
rsync -a /home/steam/Steam/steamapps/common/PalServer/Pal/Saved /home/steam/Steam/steamapps/common/PalServer/Pal/backup/Saved$(date +\%Y\%m\%d\%H\%M\%S)'
```


## update server
```linux
#!/bin/bash
pkill screen &&
su steam -c 'cd &&./steamcmd.sh +login anonymous +app_update 2394010 validate +quit ' &&

screen -S pal -X stuff "su - steam$(printf \\r)"

screen -S pal -X stuff "cd && cd Steam/steamapps/common/PalServer/ && ./PalServer.sh -useperfthreads -NoAsyncLoadingThread -UseMultithreadForDS $(printf \\r)"
```

## apply game config
```linux
 #!/bin/bash
pkill screen

screen -dmS pal
screen -S pal -X stuff "su - steam$(printf \\r)"

screen -S pal -X stuff "cd && cd Steam/steamapps/common/PalServer/ && cp DefaultPalWorldSettings.ini Pal/Saved/Config/LinuxServer/PalWorldSettings.ini &&./PalServer.sh -useperfthreads -NoAsyncLoadingThread -UseMultithreadForDS $(printf \\r)"
```


