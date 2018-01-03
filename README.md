<p align="center">
<img src="https://user-images.githubusercontent.com/746067/28497496-2584bf68-6f4e-11e7-829a-4ec5fb92d16c.png" alt="Træfik" title="Træfik" />
</p>


# Our setup
```
                                Linux Containers
                 +------------------------------------------------+
                 |                                                |
+-------------+  |                app1  +---------+   +---------+ |
|  INTERNET   |  |         +------------> nginx   <---> php|fpm | |
+-----+-------+  |         |            +---------+   +---------+ |
      |          |         |                                      |
      |          |         |                                      |
+-----v-------+  |  +------v---+  app2  +---------+   +---------+ |
| CloudFlare  <---->+  traefik <--------> nginx   <---> node.js | |
+-------------+  |  +----+-^---+        +---------+   +---------+ |
                 |       | |                                      |
                 |       | |                                      |
+-------------+  |       | |      app3  +---------+   +---------+ |
|Let's Encrypt<----------+ +------------> nginx   <---> lua     | |
+-------------+  |                      +---------+   +---------+ |
                 |                                                |
                 +------------------------------------------------+
```

# What Traefik does?
- Reverse proxy to `app1/2/3` (single IP, single port, multiple apps)
- Manages the SSL certs for `app1/2/3` with `Let's Encrypt (ACME)` using DNS auth with `CloudFlare`
- Traefik listen for new `Docker` events to setup new reverse proxies or generate new SSL certs automagically

