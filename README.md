[![Build Status](https://travis-ci.org/notandy/ympd.svg)](https://travis-ci.org/notandy/ympd)
ympd
====

Standalone MPD Web GUI written in C, utilizing Websockets and Bootstrap/JS


http://www.ympd.org

![ScreenShot](http://www.ympd.org/assets/ympd_github.png)

Dependencies
------------
 - libmpdclient 2: http://www.musicpd.org/libs/libmpdclient/
 - cmake 2.6: http://cmake.org/
 - OpenSSL: https://www.openssl.org/

Unix Build Instructions
-----------------------

1. install dependencies. cmake, libmpdclient (dev), and OpenSSL (dev) are available from all major distributions.
2. create build directory ```cd /path/to/src; mkdir build; cd build```
3. create makefile ```cmake ..  -DCMAKE_INSTALL_PREFIX:PATH=/usr```
4. build ```make```
5. install ```sudo make install``` or just run with ```./ympd```

Run flags
---------
```
Usage: ./ympd [OPTION]...

 -h, --host <host>             connect to mpd at host [localhost]
 -p, --port <port>             connect to mpd at port [6600]
 -w, --webport [ip:]<port>     listen interface/port for webserver [8080]
 -d, --dirbletoken <apitoken>  Dirble API token
 -u, --user <username>         drop priviliges to user after socket bind
 -V, --version                 get version
 --help                        this help
```

SSL Support
-----------
To run ympd with SSL support:

- create a certificate (key and cert in the same file), example:
```
# openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 1000 -nodes
# cat key.pem cert.pem > ssl.pem
```
- tell ympd to use a webport using SSL and where to find the certificate: 
```
# ./ympd -w "ssl://8081:/path/to/ssl.pem"
```

Docker configuration
--------------------

To build the ympd app into a docker image:

```
docker build -t pacruz-ympd .
docker save pacruz-ympd > pacruz-ympd.tar
```

To run the container with docker compose, the following compose file should work

```
services:
  ympd:
    image: pacruz-ympd
    container_name: pacruz-ympd
    environment:
      MPD_HOSTNAME: "<IP_ADDRESS>"
      MPD_PORT: "6600"
    ports:
      - 8080:8080
    restart: unless-stopped
```

Then run 
```
docker compose up -d
```

Updates made for build errors
-----------------------------

https://github.com/notandy/ympd/issues/193

Copyright
---------

2013-2014 <andy@ndyk.de>
