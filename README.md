#Calibre GUI and Server

Run the Calibre X app accessible in a web browser

##Install On unRaid:

On unRaid, install from the Community Repositories and enter the app folder location and the port for the webUI.


##Install On Other Platforms (like Ubuntu, Synology 5.2 DSM, etc.):

On other platforms, you can run this docker with the following command:

```
docker run -d --name="RDP-Calibre" -e EDGE="0" -e WIDTH="1280" -e HEIGHT="720" -v /path/to/config:/config:rw -v /etc/localtime:/etc/localtime:ro -p XXXX:8080 -p YYYY:8081 aptalca/docker-rdp-calibre
```

###Setup Instructions
- Replace the variable "/path/to/config" with your choice of folder on your system. That is where the config and the library files will reside, and they will survive an update, reinstallation, etc. of the container.
- Change "XXXX" to a port of your choice, it will be the port for the main Calibre GUI
- Change "YYYY" to a port of your choice, it will be the port for the Calibre webserver
- If you would like to have the latest updates, change the EDGE variable to "1", and the container will update calibre to the latest version every time it is restarted
- If you'd like to change the resolution for the GUI, you can modify the WIDTH and HEIGHT variables
- IMPORTANT: On first start, select "/config" as the library location in the Calibre wizard

You can access the GUI by pointing your web browser to http://SERVERIP:XXXX/#/client/c/Calibre

You can access the Calibre webserver by pointing your web browser to http://SERVERIP:YYYY

(Replace SERVERIP, XXXX and YYYY with your values)

###Advanced Features (only for docker pros)
####Custom library location:
If you would like to change the library location you need to do a couple of things:
- First add a new mount point for the library location in the docker run command. Example: -v /path/to/library:/library:rw
- Then add an environment variable (LIBRARYINTERNALPATH) to specify the internal library location for the webserver. Example: -e LIBRARYINTERNALPATH="/library"
- When you fire up calibre the first time select your library location. Example: /library
####URL Prefix for reverse proxy:
- Add an environment variable (URLPREFIX) to docker run to specify the url prefix for the webserver. Example: -e URLPREFIX="/calibre"
- To access the webserver, go to http://SERVERIP:YYYY/calibre
