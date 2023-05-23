# my-SearXNG-Docker-Compose
Create a SearXNG Instance in 5 minutes using docker-compose.

## Security Audits:

- [Internet.ml](https://internet.nl/site/search.whateveritworks.org/2060148/)
- [HSTS Preload](https://hstspreload.org/)
- [SSL Labs](https://www.ssllabs.com/ssltest/analyze.html?d=search.whateveritworks.org)
- [Security Headers](https://securityheaders.com/?q=search.whateveritworks.org&hide=on&followRedirects=on)
- [pagespeed](https://pagespeed.web.dev/)
- [webbkoll](https://webbkoll.dataskydd.net/en)
- [ImmuniWeb](https://www.immuniweb.com/ssl/search.whateveritworks.org/a8FxuGr6/)
- [HSTS Preload](https://hstspreload.org/)

## Usage:

1. Buy [Hetzner.com](https://hetzner.com) it's 100% renewal hardware and you get affordable dedicated servers, and you also help save the world.

2. ```apt install git```

3. ```git clone https://github.com/WhateverItWorks/searxng-docker.git searxng```

4. ```nano settings.yml```

5. ```nano docker-compose.yml```

6. ```docker-compose up -d```


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
