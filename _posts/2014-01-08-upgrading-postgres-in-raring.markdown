---
layout: note
title: Upgrading Postgres in Raring
date: 2014-01-08
categories: postgres linux upgrade
---

Note that this method is basically brute force.

## Remove

```bash
export PKGS='^(postg.*|pgadmin.*|.*qgis.*|libgdal.*)$'

sudo dpkg --purge --force-depends $(dpkg --get-selections | grep -P "${PKGS}"  | awk '{print $1}')
```

## Reinstall

See [here](http://trac.osgeo.org/postgis/wiki/UsersWikiPostGIS21UbuntuPGSQL93Apt), or short version. Lie and say we're using precise even though we're using raring:

```bash
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main" >> /etc/apt/sources.list'

wget --quiet -O - http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc | sudo apt-key add -

sudo apt-get update

sudo apt-get install Postgresql-9.3-postgis pgadmin3 postgresql-contrib
```
