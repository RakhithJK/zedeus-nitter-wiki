# **Nitter – Unraid Docker Installation**

_Please note - For Unraid, I have released a 'Community Apps' template which has simplified the installation of Nitter on your device allowing you to jump to step 15 once you have found Nitter in the Community Apps page. However, if you wish to install directly from DockerHub yourself you can continue to follow these steps._

This Unraid Docker Installation guide will mostly assume a few things;
1.	You have docker enabled within Unraid
2.	You have enabled community apps within Unraid
3.	You have enabled within settings the ability to utilize dockerhub for search results (_see settings within apps tab_)
4.	_OPTIONAL - You have a reverse proxy container and network to allow for certificate handling & SSL connections_


With that in mind, the installation of Nitter is rather simple once you have the above setup.


5.	Head over to apps and search for Nitter, click the 'Click Here To Get More Results From DockerHub' hyperlink to give more results.
6.	Click to begin the installation of Nitter within the search result. (_The repo is zedeus/nitter_)
7.	Set the toggle on the right in the template as ‘advanced view’ (_It defaults to basic view_)
8.	Set your ‘Icon URL’ as https://raw.githubusercontent.com/zedeus/nitter/master/public/logo.png (_This will provide you with the Nitter logo_)
9.	Set your ‘WebUI’ as http://[IP]:[PORT:8080]/ (_This could be changed to whatever suits your local server port requirements - see below_)
10.	Set ‘Extra Parameters’ as --restart=always
11.	Set your network type as needed (_OPTIONAL - Set network type as your network that you utilize for your SSL certs (for me its proxnetwork).)_
12.	Add in your static IP address that you will utilize for Nitter. (_This can be configured to suit your reverse proxy. You can even leave it empty if that's easier. I found in my setup that it was easier for me to have the IP set as a static entry._)

13.	Add in a ‘path’ as;

- Name – Appdata
- Container Path - /config
- Host Path - /mnt/user/appdata/nitter (_this could be changed to whatever suits your local server path requirements if your appdata path is different_)
- Default Value - /mnt/user/appdata/nitter (_see above_)
- Acccess Mode – Read/Write
- Description – Appdata location

14.	Now add in a ‘port’ as;

- Name – Port
- Container Port – 8080
- Host Port – 8080 (_this could be changed to whatever suits your local server port requirements if your 8080 is already in use_)
- Default Value – 8080 (_this could be changed to whatever suits your local server port requirements - as above_)
- Connection Type – TCP
- Description – Container Port: 8080

15.	Uncheck the ‘Start Container After Install’ checkbox. (_We need to add the nitter.conf prior to starting the container_)
16.	Click apply to download/install the container.

17.	Now to generate the required ‘nitter.conf;’

- Enter terminal from the webGUI of Unraid and navigate over to /mnt/user/appdata/nitter
- Use your terminal text editor of choice (vi or nano)
  _For example – nano nitter.conf_
- Paste in the following nitter.conf (_this should initially be the same as the one listed https://github.com/zedeus/nitter/blob/master/nitter.conf_)

```
[Server]
address = "0.0.0.0"
port = 8080
https = false  # disable to enable cookies when not using https
httpMaxConnections = 100
staticDir = "./public"
title = "nitter"
hostname = "nitter.net"

[Cache]
listMinutes = 240  # how long to cache list info (not the tweets, so keep it high)
rssMinutes = 10  # how long to cache rss queries
redisHost = "localhost"
redisPort = 6379
redisConnections = 20 # connection pool size
redisMaxConnections = 30
redisPassword = ""
# max, new connections are opened when none are available, but if the pool size
# goes above this, they're closed when released. don't worry about this unless
# you receive tons of requests per second

[Config]
hmacKey = "secretkey" # random key for cryptographic signing of video urls
base64Media = false # use base64 encoding for proxied media urls
tokenCount = 10
# minimum amount of usable tokens. tokens are used to authorize API requests,
# but they expire after ~1 hour, and have a limit of 187 requests.
# the limit gets reset every 15 minutes, and the pool is filled up so there's
# always at least $tokenCount usable tokens. again, only increase this if
# you receive major bursts all the time

# Change default preferences here, see src/prefs_impl.nim for a complete list
[Preferences]
theme = "Nitter"
replaceTwitter = "nitter.net"
replaceYouTube = "piped.kavin.rocks"
replaceInstagram = ""
proxyVideos = true
hlsPlayback = false
infiniteScroll = false
```

18. Start your Nitter docker container
19. _OPTIONAL – Head over to your SSL cert provider container of choice and set-up as necessary to server certs to your Nitter instance for your domain_.