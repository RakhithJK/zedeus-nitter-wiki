### Example Configuration
```
server {
	listen 443 ssl;
	server_name YOUR_DOMAIN_NAME;
	ssl_certificate YOUR_SSL_CERT;
	ssl_certificate_key YOUR_SSL_CERT_KEY;
	ssl_protocols TLSv1.2 TLSv1.1 TLSv1;
	ssl_prefer_server_ciphers on;
	ssl_ciphers "EECDH+ECDSA+AESGCM EECDH+aRSA+AESGCM EECDH+ECDSA+SHA384 EECDH+ECDSA+SHA256 EECDH+aRSA+SHA384 EECDH+aRSA+SHA256 EECDH+aRSA+RC4 EECDH EDH+aRSA RC4 !aNULL !eNULL !LOW !3DES !MD5 !EXP !PSK !SRP !DSS";

	# Security Headers
	add_header Strict-Transport-Security "max-age=31536000; includeSubDomains preload" always;
	add_header Content-Security-Policy "default-src 'none'; script-src 'self' 'unsafe-inline'; img-src 'self'; style-src 'self' 'unsafe-inline'; font-src 'self'; object-src 'none'; media-src 'self' blob:; worker-src 'self' blob:; base-uri 'self'; form-action 'self'; frame-ancestors 'self'; connect-src 'self' https://*.twimg.com; manifest-src 'self'";
	add_header X-Content-Type-Options nosniff;
	add_header X-Frame-Options DENY;
	add_header X-XSS-Protection "1; mode=block";

	location / {
		proxy_pass http://localhost:YOUR_NITTER_PORT;
	}

	location = /robots.txt {
		add_header Content-Type text/plain;
		return 200 "User-agent: *\nDisallow: /\n";
	}
}
```