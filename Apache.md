If you are not already running apache, or are using docker, it is recommended that you use [nginx](Nginx) instead of apache. However, nitter will still work well behind apache if that is your preference.

Below is a sample configuration that forces users to use `https` which proxies a connection to nitter. Be sure to have `proxy_http` enabled (ie `a2enmod proxy_http`), or this configuration will not work.

```
<VirtualHost *:80>                                                                   
    ServerName nitter.example.com                                                    
                                                                                     
    # force https                                                                    
    Redirect / https://nitter.example.com/                                           
                                                                                     
    # logging                                                                        
    ErrorLog ${APACHE_LOG_DIR}/nitter.error.log                                      
    CustomLog ${APACHE_LOG_DIR}/nitter.access.log combined                           
</VirtualHost>

<IfModule mod_ssl.c>
    <VirtualHost *:443>
        ServerName nitter.example.com

        # logging
        ErrorLog ${APACHE_LOG_DIR}/nitter.error.log
        CustomLog ${APACHE_LOG_DIR}/nitter.access.log combined

        # Nitter Proxy configuration
        ProxyPreserveHost On
        ProxyPass / http://127.0.0.1:8181/ nocanon
        ProxyPassReverse / http://127.0.0.1:8181/
        AllowEncodedSlashes On

        # Lets Enctrypt TLS Settings
        SSLEngine on
        SSLCertificateFile /etc/letsencrypt/live/nitter.example.com/fullchain.pem
        SSLCertificateKeyFile /etc/letsencrypt/live/nitter.example.com/privkey.pem
        Include /etc/letsencrypt/options-ssl-apache.conf

    </VirtualHost>
</IfModule>

```