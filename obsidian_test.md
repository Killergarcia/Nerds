## Installing steamcmd

```
sudo useradd -m steam
sudo passwd steam
	Set password for the "steam" profile
```

~~Back out to cs2-server (sudoer)~~

```
sudo add-apt-repository multiverse; sudo dpkg --add-architecture i386; sudo apt update
sudo apt install steamcmd
```

Login with Steam user we made earlier
```
sudo -u steam -s
cd /home/steam
```

SteamCMD won't run yet because we installed it using the other user, so the  linux `steam` user's $PATH variable needs to be updated. As the linux `steam` user, run:

```
nano ~/.bashrc
```

Then at the bottom, add:

```
# Adding steamcmd paths to $PATH
export PATH=/usr/games/:$PATH
```

*As a note, this is stupid. The VDC docs are like "oh no running steamcmd as sudo is a risk" but then you can't install it from the non-sudoer `steam` account but then installing from another account doesn't update all users' $PATH. Dumb.*

Log out of the `steam` user and come back
```
exit
sudo -u steam -s
```

Create a directory for CS2 DS to install to:

```
cd /home/steam
mkdir cs2-ds
```

Run steamcmd
	It will update

At the `Steam>` prompt, run:
```
force_install_dir /home/steam/cs2-ds
```

Login to steam (We don't need to login with our actual account) and install CS2 DS app
```
login anonymous
app_update 730 validate
```
 It do be takin time tho

### Make a symlink because steamclient.so is put int the wrong place by default

```
ln -s /home/azureuser/.steam/steamcmd/linux32/steamclient.so /home/azureuser/.steam/sdk32/steamclient.so

ln -s /home/azureuser/.steam/steamcmd/linux64/steamclient.so /home/azureuser/.steam/sdk64/steamclient.so

mkdir /home/azureuser/.steam/sdk64/
```

## Launch CS2 DS

```
~/.steam/SteamApps/common/Counter-Strike\ Global\ Offensive/game/bin/linuxsteamrt64/cs2 -dedicated +ip 172.190.80.233 +game_type 0 +game_mode 0 +map de_dust2 +sv_setsteamaccount [GSLT] -net_port_try 1 -high -maxplayers 64 -insecure -usercon

~/.steam/SteamApps/common/Counter-Strike\ Global\ Offensive/game/bin/linuxsteamrt64/cs2 -dedicated +map de_dust2 +sv_setsteamaccount [GSLT] -net_port_try 1
```
