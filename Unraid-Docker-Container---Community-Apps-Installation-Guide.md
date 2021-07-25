# **Nitter – Unraid Docker Installation**

This Unraid Docker Installation guide will mostly assume a few things;
1.	You have docker enabled within Unraid
2.	You have enabled community apps within Unraid
3.	You have enabled within settings the ability to utilize dockerhub for search results (_see settings within apps tab_)
4.	_OPTIONAL - You have a reverse proxy container and network to allow for certificate handling & SSL connections_


With that in mind, the installation of Nitter is rather simple once you have the above setup.


5.	Head over to apps and search for Nitter
6.	Click to begin the installation of Nitter within the search result. (_The repo is zedeus/nitter_)
7.	Set the toggle on the right in the template as ‘advanced view’ (_It defaults to basic view_)
8.	Set your ‘Icon URL’ as https://github.com/zedeus/nitter/blob/master/public/logo.png?raw=true (_This will provide you with the Nitter logo_)
9.	Set your ‘WebUI’ as http://[IP]:[PORT:8080]/ (_This could be changed to whatever suits your local server port requirements - see below_)
10.	Set ‘Extra Parameters’ as --restart=always
11.	Set your network type as needed (_OPTIONAL - Set network type as your network that you utilize for your SSL certs (for me its proxnetwork).)_
12.	Add in your static IP address that you will utilize for Nitter. (_It makes it easier to get to your hosted instance_)

13.	Add in a ‘path’ as;

- Name – Appdata
- Container Path - /config
- Host Path - /mnt/user/appdata/nitter
- Default Value - /mnt/user/appdata/nitter
- Acccess Mode – Read/Write
- Description – Appdata location

14.	Add in a ‘variable’ as;

- Name – PUID
- Key - PUID
- Value – 99
- Default Value - 99
- Description – PUID

15.	Add in a further ‘variable’ as;

- Name – PGID
- Key – PGID
- Value – 100
- Default Value – 100
- Description – PGID

16.	Now add in a ‘port’ as;

- Name – Port
- Container Port – 8080
- Host Port – 8080 (_this could be changed to whatever suits your local server port requirements if your 8080 is already in use_)
- Default Value – 8080 (_this could be changed to whatever suits your local server port requirements - as above_)
- Connection Type – TCP
- Description – Container Port: 8080

17.	Uncheck the ‘Start Container After Install’ checkbox. (_We need to add the nitter.conf prior to starting the container_)
18.	Click apply to download/install the container.

19.	Now to generate the required ‘nitter.conf;’

- Enter terminal from the webGUI of Unraid and navigate over to /mnt/user/appdata/nitter
- Use your terminal text editor of choice (vi or nano)
  _For example – nano nitter.conf_
- Paste in the following nitter.conf (_this is the same as the one listed on the installation guide in Nitter's readme_)

```
[Unit]
Description=Nitter (An alternative Twitter front-end)
After=syslog.target
After=network.target

[Service]
Type=simple

# set user and group
User=nitter
Group=nitter

# configure location
WorkingDirectory=/home/nitter/nitter
ExecStart=/home/nitter/nitter/nitter

Restart=always
RestartSec=15

[Install]
WantedBy=multi-user.target
```

20. Start your Nitter docker container
21. _OPTIONAL – Head over to your SSL cert provider container of choice and set-up as necessary to server certs to your Nitter instance for your domain_.