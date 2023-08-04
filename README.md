# my-SearXNG-Docker-Compose
Create a SearXNG Instance in 5 minutes using docker-compose.

## Security Audits:

- [Internet.nl](https://internet.nl/site/search.whateveritworks.org/2060148/)
- [HSTS Preload](https://hstspreload.org/)
- [SSL Labs](https://www.ssllabs.com/ssltest/analyze.html?d=search.whateveritworks.org)
- [Security Headers](https://securityheaders.com/?q=search.whateveritworks.org&hide=on&followRedirects=on)
- [pagespeed](https://pagespeed.web.dev/)
- [webbkoll](https://webbkoll.dataskydd.net/en)
- [ImmuniWeb](https://www.immuniweb.com/ssl/search.whateveritworks.org/uLlrAeMb/)
- [Hardenize](https://www.hardenize.com/report/search.whateveritworks.org/1686343966)
- [Mozilla.org](https://observatory.mozilla.org/)
- [report-uri.com](https://report-uri.com/home/tools)
- [check-your-website.server-daten.de](https://check-your-website.server-daten.de/?q=search.whateveritworks.org)
- [csp-evaluator.withgoogle.com](https://csp-evaluator.withgoogle.com/)
- [OpenWPM](https://github.com/openwpm/OpenWPM)
- [privacyscore.org](https://privacyscore.org/)

## Usage:

1. Buy [Hetzner.com](https://hetzner.com) it's 100% renewal hardware and you get affordable dedicated servers, and you also help save the world.

2. ```apt install git```

3. ```git clone https://github.com/WhateverItWorks/SearXNG-Reworked searxng```

4. ```nano searxng/settings.yml```

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

### Advanced

- [Enable Google TCP BBR](https://www.linuxbabe.com/ubuntu/enable-google-tcp-bbr-ubuntu)
- [Setup Local Resolver: 127.0.0.1](https://www.linuxbabe.com/ubuntu/set-up-local-dns-resolver-ubuntu-20-04-bind9)
