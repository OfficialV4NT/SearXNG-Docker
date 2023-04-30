# my-SearXNG-Docker-Compose
Create a SearXNG Instance in 5 minutes using docker-compose.

Official Instance

| Domain | CDN/DDoS Protection | Provider | Country |
| -- | -- | -- | -- |
| [search.xbdm.fun](https://search.xbdm.fun) | Cloudflare | Hetzner | Germany

**Make a PR or issue to get added to the list.**

## Security Audits:

- [Internet.ml](https://internet.nl/site/search.xbdm.fun/2060148/)
- [Mozilla.org](https://observatory.mozilla.org/)
- [ImmuniWeb](https://www.immuniweb.com/ssl/search.xbdm.fun/a8FxuGr6/)
- [HSTS Preload](https://hstspreload.org/)
- [SSL Labs](https://www.ssllabs.com/ssltest/analyze.html?d=search.xbdm.fun)
- [Security Headers](https://securityheaders.com/?q=search.xbdm.fun&hide=on&followRedirects=on)


## Usage:

1. Buy [Hetzner.com](https://hetzner.com) it's 100% renewal hardware and you get affordable dedicated servers, and you also help save the world.

2. Get [Cloudflare](https://cloudflare.com) it's carbon renewal and you help save the world.

2. ```apt install git```

3. ```git clone https://github.com/WhateverItWorks/searxng-docker.git searxng```

4. ```nano settings.yml```

5. ```nano docker-compose.yml```

5. ```docker-compose up -d```


```http://localhost:8071```


### How to access the debugging logs:

To access the logs of one specific container:
- SearXNG: `docker-compose logs -f searxng`
- Redis: `docker-compose logs -f redis`


### To update the SearXNG stack:

```sh
docker-compose down
docker-compose pull
docker-compose up -d
```
