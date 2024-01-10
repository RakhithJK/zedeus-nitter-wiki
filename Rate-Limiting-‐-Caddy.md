# Mitigating Unauthorized Web Scraping Bot Traffic

The current design of Nitter, along with its methodology for accessing the Twitter service, necessitates heightened vigilance on the part of instance operators to manage unwarranted access by web scraping bots. This guide is intended to provide operators with essential information to effectively mitigate unauthorized web scraping bot traffic.

## Prerequisites

Before proceeding with the rate-limiting setup, ensure that you have:

1. A functional Nitter installation.
2. Caddy as your web server, with an installation of the custom module [RussellLuo/caddy-ext/ratelimit](https://github.com/RussellLuo/caddy-ext/tree/master/ratelimit). You can refer to the [Caddy docs](https://caddyserver.com/docs/build) or its [docker docs](https://hub.docker.com/_/caddy#Adding%20custom%20Caddy%20modules) for instructions.
3. In this guide, we will add rate-limiting rules to the server block as outlined in [Caddy Configuration](https://github.com/zedeus/nitter/wiki/Caddy).


## Rate Limiting Configuration

__Caddyfile__
```
nitter.example.com {
	@notstatic {
		not path /css/* /js/* /fonts/* /browserconfig.xml /android-chrome* /favicon* /logo* /lp.svg /robots.txt /safari* /site.webmanifest /pic/*
	}
	rate_limit @notstatic {remote.ip} 2r/s 60000 500
	rate_limit @notstatic {remote.ip} 30r/m 300000 500
	reverse_proxy localhost:8080 {
		transport http {compression off}
	}
	header {
		Strict-Transport-Security "max-age=63072000"
		Referrer-Policy no-referrer
		X-Permitted-Cross-Domain-Policies none
		X-Content-Type-Options nosniff
		Permissions-Policy "Permissions-Policy: accelerometer=(), ambient-light-sensor=(), autoplay=(self), battery=(), camera=(), cross-origin-isolated=(), display-capture=(), document-domain=(), encrypted-media=(), execution-while-not-rendered=(), execution-while-out-of-viewport=(), fullscreen=(self), geolocation=(), gyroscope=(), keyboard-map=(), magnetometer=(), microphone=(), midi=(), navigation-override=(), payment=(), picture-in-picture=(self), publickey-credentials-get=(), screen-wake-lock=(), sync-xhr=(), usb=(), web-share=(), xr-spatial-tracking=()"
		header Content-Security-Policy "default-src 'none'; script-src 'self' 'unsafe-inline'; img-src 'self'; style-src 'self' 'unsafe-inline'; font-src 'self'; object-src 'none'; media-src 'self' blob:; worker-src 'self' blob:; base-uri 'self'; form-action 'self'; frame-ancestors 'self'; connect-src 'self' https://*.twimg.com; manifest-src 'self'"
	}
	# Optional: discard logs completely
	log {
		output discard

	}
}
```

The `@notstatic` named matcher ensure that normal usage, such as serving images, videos, and site data, does not trigger rate limiting. 

The `rate_limit` directives limits users to 2 request per second and 30 requests per minute, a natural browsing rate for the site.

Over this, you need to setup fail2ban to persist the bans. Follow https://muetsch.io/how-to-integrate-caddy-with-fail2ban.html and the Fail2Ban instructions under https://github.com/zedeus/nitter/wiki/Rate-Limiting-%E2%80%90-Nginx#fail2ban to do so. (Do note you need logs enabled for fail2ban)

## Alternative module

You may also use the module [mholt/caddy-ratelimit](https://github.com/mholt/caddy-ratelimit) to manage unwarranted access.