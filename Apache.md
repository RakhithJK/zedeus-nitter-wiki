If you are not already running Apache, or are using Docker, it is recommended that you use [nginx](Nginx) instead of Apache. However, Nitter will still work well behind Apache if that is your preference.

Below is a sample configuration that forces users to use `https` which proxies a connection to Nitter. Be sure to have `proxy_http` enabled (ie `a2enmod proxy_http`), or this configuration will not work.

```
<VirtualHost *:80>                                                                   
    ServerName YOUR_DOMAIN                                                    
                                                                                     
    # force https                                                                    
    Redirect / https://YOUR_DOMAIN                                          
                                                                                     
    # logging                                                                        
    ErrorLog ${APACHE_LOG_DIR}/nitter.error.log                                      
    CustomLog ${APACHE_LOG_DIR}/nitter.access.log combined                           
</VirtualHost>

<IfModule mod_ssl.c>
    <VirtualHost *:443>
        ServerName YOUR_DOMAIN

        # Logging
        ErrorLog ${APACHE_LOG_DIR}/nitter.error.log
        CustomLog ${APACHE_LOG_DIR}/nitter.access.log combined

        # Nitter Proxy Configuration
        ProxyPreserveHost On
        ProxyPass / http://127.0.0.1:NITTER_PORT/ nocanon
        ProxyPassReverse / http://127.0.0.1:NITTER_PORT/
        AllowEncodedSlashes On

        # Lets Encrypt TLS Settings
        SSLEngine on
        SSLCertificateFile /etc/letsencrypt/live/YOUR_DOMAIN/fullchain.pem
        SSLCertificateKeyFile /etc/letsencrypt/live/YOUR_DOMAIN/privkey.pem
        Include /etc/letsencrypt/options-ssl-apache.conf

    </VirtualHost>
</IfModule>

```