# Example config
```
nitter.example.com {
	header {
		Strict-Transport-Security "max-age=63072000"
		Referrer-Policy no-referrer
		X-Permitted-Cross-Domain-Policies none
		X-Content-Type-Options nosniff
		Permissions-Policy "Permissions-Policy: accelerometer=(), ambient-light-sensor=(), autoplay=(self), battery=(), camera=(), cross-origin-isolated=(), display-capture=(), document-domain=(), encrypted-media=(), execution-while-not-rendered=(), execution-while-out-of-viewport=(), fullscreen=(self), geolocation=(), gyroscope=(), keyboard-map=(), magnetometer=(), microphone=(), midi=(), navigation-override=(), payment=(), picture-in-picture=(self), publickey-credentials-get=(), screen-wake-lock=(), sync-xhr=(), usb=(), web-share=(), xr-spatial-tracking=()"
		header Content-Security-Policy "default-src 'none'; script-src 'self' 'unsafe-inline'; img-src 'self'; style-src 'self' 'unsafe-inline'; font-src 'self'; object-src 'none'; media-src 'self' blob:; worker-src 'self' blob:; base-uri 'self'; form-action 'self'; frame-ancestors 'self'; connect-src 'self' https://*.twimg.com; manifest-src 'self'"
	}
	reverse_proxy http://localhost:8080 {
		transport http {
			compression off
		}
	}
	# Optional: discard logs completely
	log {
		output discard

	}
}
```