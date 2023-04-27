# searxng-docker

Create a new SearXNG  instance in five minutes using Docker


## Security Audits:

- [Internet.ml](https://internet.nl/site/code.xbdm.fun/2060148/)
- [Mozilla.org](https://observatory.mozilla.org/)
- [ImmuniWeb](https://www.immuniweb.com/ssl/code.xbdm.fun/a8FxuGr6/)
- [HSTS Preload](https://hstspreload.org/)
- [SSL Labs](https://www.ssllabs.com/ssltest/analyze.html?d=code.xbdm.fun)
- [Security Headers](https://securityheaders.com/?q=code.xbdm.fun&hide=on&followRedirects=on)


## Usage:

1. Buy [Hetzner.com](https://hetzner.com) it's 100% renewal hardware and you get affordable dedicated servers, and you also help save the world.

2. Get [Cloudflare](https://cloudflare.com) it's carbon renewal and you help save the world.

2. ```apt install git```

3. ```git clone https://github.com/WhateverItWorks/searxng-docker.git searxng```

4. ```nano docker-compose.yml (the settings that im using should be recommended for you, but you can change it if you want)```

5. ```docker-compose up -d```



```http://localhost:8088```


## How to access the logs
To access the logs from all the containers use: `docker-compose logs -f`.

To access the logs of one specific container:
- SearXNG: `docker-compose logs -f searxng`
- Redis: `docker-compose logs -f redis`



## Note on the image proxy feature

The SearXNG image proxy is activated by default.

The default [Content-Security-Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) allow the browser to access to ```${SEARXNG_HOSTNAME}``` and ```https://*.tile.openstreetmap.org;```.


## How to update ?

To update the SearXNG stack:

```sh
docker-compose pull
docker-compose down
docker-compose up -d
```

To update this `nano docker-compose.yml` file:

Check out the newest version on github: [searxng/searxng-docker](https://github.com/searxng/searxng-docker).
