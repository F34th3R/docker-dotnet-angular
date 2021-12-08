# Docker 🐋, Dotnet and Angular (nginx using proxy)

## Client config

For Nginx

proxy_pass http://**test_server:5000**/weatherforecast;

```nginx.conf
location /weatherforecast {
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-NginX-Proxy true;
    proxy_pass http://test_server:5000/weatherforecast;
    proxy_ssl_session_reuse off;
    proxy_set_header Host $http_host;
    proxy_cache_bypass $http_upgrade;
    proxy_redirect off;
    # if BACKEND_URI is using TLS/SSL with SNI, this is important!
    proxy_ssl_server_name on;
  }
```

For Angular.json

```json
...
	"serve": {
		"builder": ...,
		"options": {
			"browserTarget": "client:build",
			"proxyConfig": "src/proxy.conf.json"
			},
		...
```
