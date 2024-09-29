# D2GS-under-Wine-5.0
How to execute D2GS under Wine 5.0


I recently had major problems with crashes and attacks when using the D2GS version with Wine 2.0.1.

I soon discovered that this loophole to lock rooms only occurred in this version of Wine 2.0.1, giving a loophole for malicious people to prevent the creation of rooms on my game server.

So with the help of the community, I'm publishing here the guide for you to use D2GS in Wine 5.0 which is very stable and safe because in addition to allowing you to use IPTables rules to block malicious packets and sploits, there are no flaws.

## Requirements
```
OS: Ubuntu 18.04.6 LTS
D2GS: Version 1.13c
Wine: Version 5.0
```

## Swap file
If your machine has 512 Mb of RAM, it is possible that your wine build will freeze. To avoid that you might want to add some
swap memory.

On Ubuntu Ubuntu 18.04.6 LTS:
```
free -m
```
If the output looks something like this, 
```
root@vps:~# free -m
              total        used        free      shared  buff/cache   available
Mem:            512         x           x           x         x          x
Swap:            0          0           0           0         0          0
```
that means you machine doesn't have Swap memory. Execute the following comamnds to add 1 Gb to Swap.
```
dd if=/dev/zero of=/swapfile bs=1024 count=1048576
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
```

### Step 1 - Install the dependencies
Using Ubuntu in terminal with a user and having sudo permissions, run the following commands to install the dependencies.
```
sudo dpkg --add-architecture i386
sudo apt-get update -y
sudo apt-get install flex
sudo apt-get install bison
sudo apt-get install -y lib32ncurses5 lib32z1 gcc-multilib g++-multilib xserver-xorg-dev:i386 libfreetype6-dev:i386
```

### Step 2 - Get sock.c and Wine 5.0
Get changed sock.c for D2GS to work and Wine 5.0 version.
```

wget http://dl.winehq.org/wine/source/5.0/wine-5.0.tar.xz
wget https://raw.githubusercontent.com/rodolfoorl/D2GS-under-Wine-5.0/main/sock.c
```

### Step 3 - Make and Install
Change the Wine source code sock.c and organize the folders to compile the Wine source code.
```
tar xf wine-5.0.tar.xz
mv sock.c wine-5.0/server
mv wine-5.0 wine-source
mkdir wine-dirs
mv wine-source wine-dirs
cd wine-dirs
mkdir wine-build
cd wine-build
../wine-source/configure --without-freetype
make
sudo make install
```

### Step 4 - Get D2GS and Configure *.reg
Now you should get the D2GS with your MPQ get and configure the D2GS for IP.
```
#After preparing the D2GS files in a folder and having configured d2gs.reg, run it with this command inside the D2GS folder.
wine regedit d2gs.reg

#And execute D2GS.exe
wine D2GS.exe
```
Follow the same guide on Github. Good fun everyone!
