# Example config
```
nitter.example.com {
	header {
		Strict-Transport-Security "max-age=63072000"
		Referrer-Policy no-referrer
		X-Permitted-Cross-Domain-Policies none
		X-Content-Type-Options nosniff
		Permissions-Policy "Permissions-Policy: accelerometer=(), ambient-light-sensor=(), autoplay=(self), battery=(), camera=(), cross-origin-isolated=(), display-capture=(), document-domain=(), encrypted-media=(), execution-while-not-rendered=(), execution-while-out-of-viewport=(), fullscreen=(self), geolocation=(), gyroscope=(), keyboard-map=(), magnetometer=(), microphone=(), midi=(), navigation-override=(), payment=(), picture-in-picture=(self), publickey-credentials-get=(), screen-wake-lock=(), sync-xhr=(), usb=(), web-share=(), xr-spatial-tracking=()"
		Content-Security-Policy "default-src 'none'; script-src 'self'; img-src 'self'; style-src 'self'; media-src 'self'; manifest-src 'self'; base-uri 'self'; form-action 'self'; frame-ancestors 'none'"
	}
	reverse_proxy http://localhost:8080 {
		transport http {
			compression off
		}
	}
}
```