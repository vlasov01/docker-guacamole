[![Docker Build Status](https://img.shields.io/docker/build/oznu/guacamole.svg?label=x64%20build)](https://hub.docker.com/r/oznu/guacamole/) [![Travis](https://img.shields.io/travis/oznu/docker-guacamole.svg?label=arm%20build)](https://travis-ci.org/oznu/docker-guacamole) [![Docker Pulls](https://img.shields.io/docker/pulls/oznu/guacamole.svg)](https://hub.docker.com/r/oznu/guacamole/)

# Docker Guacamole for RPi

A Docker Container for [Apache Guacamole](https://guacamole.apache.org/), a client-less remote desktop gateway. It supports standard protocols like VNC, RDP, and SSH over HTML5.

This image will run on most platforms that support Docker including Docker for Mac, Docker for Windows, Synology DSM and Raspberry Pi 3 boards.

[![IMAGE ALT TEXT](http://img.youtube.com/vi/esgaHNRxdhY/0.jpg)](http://www.youtube.com/watch?v=esgaHNRxdhY "Video Title")

This container runs the guacamole web client, the guacd server and a postgres database.

## Usage

```shell
docker build --tag rpi/guacamole:1.0 docker-guacamole
docker run \
  -p 8080:8080 \
  -v </path/to/config>:/config \
  rpi/guacamole:1.0
```

## Parameters

The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side.

* `-p 8080:8080` - Binds the service to port 8080 on the Docker host, **required**
* `-v /config` - The config and database location, **required**
* `-e EXTENSIONS` - See below for details.

## Enabling Extensions

Extensions can be enabled using the `-e EXTENSIONS` variable. Multiple extensions can be enabled using a comma separated list without spaces.

For example:

```shell
docker run \
  -p 8080:8080 \
  -v </path/to/config>:/config \
  -e "EXTENSIONS=auth-ldap,auth-duo"
  rpi/guacamole:1.0
```

Currently the available extensions are:

* auth-ldap - [LDAP Authentication](https://guacamole.apache.org/doc/gug/ldap-auth.html)
* auth-duo - [Duo two-factor authentication](https://guacamole.apache.org/doc/gug/duo-auth.html)
* auth-header - [HTTP header authentication](https://guacamole.apache.org/doc/gug/header-auth.html)
* auth-cas - [CAS Authentication](https://guacamole.apache.org/doc/gug/cas-auth.html)
* auth-openid - [OpenID Connect authentication](https://guacamole.apache.org/doc/gug/openid-auth.html)
* auth-totp - [TOTP two-factor authentication](https://guacamole.apache.org/doc/gug/totp-auth.html)
* auth-quickconnect - [Ad-hoc connections extension](https://guacamole.apache.org/doc/gug/adhoc-connections.html)

You should only enable the extensions you require, if an extensions is not configured correctly in the `guacamole.properties` file it may prevent the system from loading. See the [official documentation](https://guacamole.apache.org/doc/gug/) for more details.

## Default User

The default username is `guacadmin` with password `guacadmin`.

## License

Copyright (C) 2017-2020

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the [GNU General Public License](./LICENSE) for more details.
