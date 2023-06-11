```sh  
mkdir /mnt/plex/plexmediaserver
cd /var/lib
sudo mv plexmediaserver plexmediaserver.bak
sudo ln -s /mnt/plex/plexmediaserver plexmediaserver  
sudo cp -r plexmediaserver.bak/* /mnt/plex/plexmediaserver/  
sudo chown -h plex:plex plexmediaserver  
sudo rm -rf plexmediaserver.bak
```