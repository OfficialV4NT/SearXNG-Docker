# SearXNG Docker

SearXNG is a free internet metasearch engine which aggregates results from more than 70 search services. Users are neither tracked nor profiled. Additionally, SearXNG can be used over Tor for online anonymity.

# Debug

To access the ```logs``` of one ```specific container```:

1. SearXNG: ```docker-compose logs -f searxng```
2. Redis: ```docker-compose logs -f searxng-redis```

#### Additional Bot Protection

To check blocked IP Address, from ```link_token: true```:

1. Go to root ```sudo su -```.

2. Copy and paste this string: ```sudo -H journalctl -u "uwsgi@searxng" | grep -o 'BLOCK: .* SUSPICIOUS_IP_WINDOW' | sudo sort -u > suspicious_ip_list.txt```.

# Deployment

The more hosted instances of SearXNG-Docker we have, the better load will be balanced between them all, leading to a better experience for everyone.

### Pre-requisites

- Server or an always-on computer
- Fast internet connection

### Dependencies
SearXNG-Docker is deployed using Docker. Docker containerizes the app for a more convenient and secure deployment.

### Install Docker

If you don't have Docker already, follow the [official documentation](https://docs.docker.com/engine/install/) to install the engine.

### Alternative: Use the pre-built Docker image

Follow the documentation here: https://hub.docker.com/r/searxng/searxng

### Clone the repo

1. Find our directory to put our SearXNG-Docker's source code.
2. Clone the repo with ```git clone https://github.com/WhateverItWorks/SearXNG-Reworked.git searxng```.
3. Edit ```settings.yml``` to your own settings.

### Setup Docker-Compose

SearXNG-Docker provides an example ```docker-compose``` file in ```docker-compose.yml```. This defines the setup for the container.

1. Modify ports if needed.
2. Usually you want to edit the ```ports:``` section to meet your needs, especially if you're using a reverse proxy, like nginx. Try replacing the ```- 80:8080``` part with - ```127.0.0.1:8071:8080```.

### Build and deploy
In the same directory as the ```docker-compose.yml``` file, run ```docker-compose up -d``` to run the container in the background as a daemon (```-d```).

### Install nginx

You can install it for your operating system according to the [official documentation](https://www.nginx.com/resources/wiki/start/topics/tutorials/install/).

### Setup the config file

Depending on your operating system, this path may differ, but usually configs are stored in ```/etc/nginx/sites-enabled```. Navigate to this directory and create a new file called ```<domain>.conf```.

In this file, put the following:
```
server {
  server_name changethis;

    listen 443 ssl;
    listen [::]:443 ssl;
    http2 on;
    ssl_certificate /etc/letsencrypt/live/changethis/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/changethis/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;

    add_header strict_sni on;
    add_header strict_sni_header on;
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
    add_header Set-Cookie "Path=/; SameSite=Strict; HttpOnly; Secure";
    add_header Content-Security-Policy "upgrade-insecure-requests; default-src 'none'; script-src 'self'; style-src 'self' form-action 'self'; form-action 'self' https://github.com/searxng/searxng/issues/new; font-src 'self'; frame-ancestors 'self'; base-uri 'self'; connect-src 'self' https://overpass-api.de; img-src 'self' data: https://*.tile.openstreetmap.org; frame-src https://www.youtube-nocookie.com https://player.vimeo.com https://www.dailymotion.com https://www.deezer.com https://www.mixcloud.com https://w.soundcloud.com https://embed.spotify.com";
    add_header X-Frame-Options "DENY";
    add_header Clear-Site-Data "cookies";
    add_header Permissions-Policy "interest-cohort=(),accelerometer=(),ambient-light-sensor=(),autoplay=(),camera=(),encrypted-media=(),focus-without-user-activation=(),geolocation=(),gyroscope=(),magnetometer=(),microphone=(),midi=(),payment=(),picture-in-picture=(),speaker=(),sync-xhr=(),usb=(),vr=()";
    add_header Cross-Origin-Resource-Policy cross-origin;
    add_header Cross-Origin-Embedder-Policy require-corp;
    add_header Cross-Origin-Opener-Policy unsafe-none;
    resolver 127.0.0.1;

    ssl_trusted_certificate /etc/letsencrypt/live/changethis/chain.pem;
    ssl_stapling on;
    ssl_stapling_verify on;
   
    # disable all logs	
    access_log off;
    error_log /dev/null crit;

            location / {
                proxy_pass http://localhost:8071;
                proxy_set_header   Host             $host;
	        proxy_set_header   Connection       $http_connection;
                proxy_set_header   X-Real-IP        $remote_addr;
                proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
		proxy_buffering  off;
                proxy_request_buffering off;
	        proxy_buffer_size 8k;
        }
}

server {
  listen 80;
  listen [::]:80;
  server_name changethis;
  return 301 https://changethis$request_uri;
  }
```

### Reload
Run ```nginx -t``` to test your config. If all is ok, it should print the following:
```
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```
If there are no issues, reload using nginx ```-s reload```.

That's it, SearXNG-Docker should now be running at <http://localhost:8071>.


### Advanced Enhancements

- [Enable Google TCP BBR](https://www.linuxbabe.com/ubuntu/enable-google-tcp-bbr-ubuntu)
- [Setup Local Resolver: 127.0.0.1](https://www.linuxbabe.com/ubuntu/set-up-local-dns-resolver-ubuntu-20-04-bind9)
- [Automatic Install](https://github.com/OfficialV4NT/Watchtower)
- [Setup Public Key Pins](https://thecustomizewindows.com/2016/07/http-public-key-pinning-hpkp-nginx/)
- [Block a Country with NGINX](https://devcoops.com/block-visitors-by-country-in-nginx/)

## Security Audits

Audit your public or private ```SearXNG-Docker Instance``` to make sure your service is hardened against cyberattacks.

- [Cloudflare Radar](https://radar.cloudflare.com/scan)
- [Internet.nl](https://internet.nl/site/)
- [HSTS Preload](https://hstspreload.org/)
- [SSL Labs](https://www.ssllabs.com/ssltest/analyze.html?d=)
- [Security Headers](https://securityheaders.com/?q=&hide=on&followRedirects=on)
- [pagespeed](https://pagespeed.web.dev/)
- [webbkoll](https://webbkoll.dataskydd.net/en)
- [ImmuniWeb](https://www.immuniweb.com/ssl/)
- [Mozilla.org](https://observatory.mozilla.org/)
- [report-uri.com](https://report-uri.com/home/tools)
- [check-your-website.server-daten.de](https://check-your-website.server-daten.de)
- [csp-evaluator.withgoogle.com](https://csp-evaluator.withgoogle.com/)
- [Hardenize](https://www.hardenize.com)
- [OpenWPM](https://github.com/openwpm/OpenWPM)
- [XSS.Report](https://xss.report)

```Make sure to not have any duplicates headers as some we already implemented inside the code```.

### Manual

```
docker-compose down
docker-compose pull
docker-compose up -d
```

### Automatic
```
https://github.com/OfficialV4NT/Watchtower
```
