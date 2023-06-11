# Plex on Pi notes  

 1 use raspberry pi imager - DONT FORGET TO GO INTO SETTINGS AND SET UP A USER
 3 FLash SD Card  
 4 Get `SSID` and `password`  
 5 Create a `wpa_supplicant.conf` file like below  

```conf  
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
network={
  ssid="MyWiFiESSID"
  ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
  psk=wifi_password_here
}
```  

IF YOU FORGET TO SET UP A USER 
get a encrypted version of your password by running
`echo 'mypassword' | openssl passwd -6 -stdin`  

then create a `userconf.txt` file with the following
<username>:<encrypted_password>


 6 Create an `ssh` filw with no extension  
 7 Copy both of these files to the boot drive of the SD Card  
 8 Put SD Card into Pi  
 9 Turn on and ssh in using `ssh pi@raspberrypi.local` or `ssh pi@ip_address`  
 10 Update pi:   
     * `sudo apt update && sudo apt upgrade -y`  
     * `sudo apt update && sudo apt dist-upgrade -y`   
 11 Install HTTPS download transport:  
     * `sudo apt install apt-transport-https -y`  
 12 Install Plex:  
     * Go to https://www.plex.tv/media-server-downloads/#plex-app  
     * Select `Plex Media Server` and choose `Linux`  
     * Choose `Ubuntu Debian ARMv7` and copy link address  
     * run `wget` and paste in copied address  
     * Run `sudo dpkg -i <plexmedia_server>` - the one that you downloaded  
     * `sudo reboot`  
 13 Plug in harddrive  
 14 get harddrive name `sudo blkid`  
 15 create dir where to mount harddrive `mkdir /mnt/plex`  
 16 change permissions `sudo chmod 775 /mnt/plex`  
 17 Mount harddrive `sudo mount /dev/sda1 /mnt/plex`  
 18 backup `fstab` - `sudo cp /etc/fstab /etc/fstab.backup`  
 19 edit fstab so that drive will be mounted everytime pi starts `sudo vim /etc/fstab` (install vim via `sudo apt install vim -y`)  
 20 add the following to the fstab file  
     * `PART UUID=<UUID>       /mnt/plex    vfat defaults          0       0`  
     * see - https://help.ubuntu.com/community/Fstab?



```
[Device] [Mount Point] [File System Type] [Options] [Dump] [Pass]
fields

description

<device>
The device/partition (by /dev location or UUID) that contain a file system.

<mount point>
The directory on your root file system (aka mount point) from which it will be possible to access the content of the device/partition (note: swap has no mount point). Mount points should not have spaces in the names.

<file system type>
Type of file system (see LinuxFilesystemsExplained).

<options>
Mount options of access to the device/partition (see the man page for mount).

<dump>
Enable or disable backing up of the device/partition (the command dump). This field is usually set to 0, which disables it.cd 

<pass num>
Controls the order in which fsck checks the device/partition for errors at boot time. The root device should be 1. Other partitions should be 2, or 0 to disable checking.
```   

 21 reboot and check harddrive  
 22 install transmission - `sudo apt install transmission-daemon transmission-cli transmission-common -y`  
 23 stop transmission - `sudo service transmission stop`  
 24 Edit transmission settings - `sudo vim /etc/transmission-daemon/settings.json`  



 25 restart transmission  
 26 list users - `cat /etc/passwd`, groups - `groups`, groups a user belongs to - `groups <user>`    
 27 add the users to all the different groups so you dont have permission errors - `usermod -a -G group user`  
 28 - setting `umask` permission in `fstab` so have permission to write to harddrive - https://www.cyberciti.biz/tips/understanding-linux-unix-umask-value-usage.html#targetText=The%20user%20file%2Dcreation%20mode,Symbolic%20values  


/dev/sda1: LABEL="System" UUID="77CF-C5DA" TYPE="vfat" PTTYPE="atari" PARTUUID="aa713c32-01"
/mnt/plex/Media/Downloads

## ip address
se

https://forums.raspberrypi.com/viewtopic.php?t=140252



## sonarr
https://sonarr.tv/#downloads-v3-linux
