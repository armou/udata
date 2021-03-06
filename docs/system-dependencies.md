# System dependencies

## Python requirements

uData requires [Python][] 2.7 (installed by default on OSX and many Linux distributions),
its development tools and some libraries to be installed (with their headers).
Most of them might already be installed as they are common development dependencies.
The full dependencies list is:

* Pillow (Image processing)
    * libjpeg
    * zlib
    * libpng
    * libtiff
    * libfreetype
    * liblcms2
    * libopenjpeg
    * libwebp
* lxml dependencies
    * libxml2
    * libxslt
* Misc dependencies
    * liblzma (required to load GeoZones)
    * libyaml (not mandatory but speed up the yaml processing)

!!! note
    By the time this project was started, Python 3 did not have great third dependencies support
    and some requirements weren't suported yet so it was started with Python 2.7.

### Debian/Ubuntu

On any Debian-like system you can install the development tools and libraries with:

```shell
$ apt-get install build-essential pkg-config python python-dev python-pip python-virtualenv\
    libjpeg-dev zlib1g-dev libtiff5-dev libfreetype6-dev \
    liblcms2-dev libopenjpeg-dev libwebp-dev libpng12-dev \
    libxml2-dev  libxslt1-dev liblzma-dev libyaml-dev
```

### OSX/Homebrew

On Mac OSX with [Homebrew][], you can install the development tools and libraries with:

```shell
$ brew install automake autoconf libtool pkg-config python \
    libjpeg zlib libtiff freetype littlecms openjpeg webp libpng \
    libxml2 libxslt xz libyaml
```

## MongoDB, ElasticSearch and Redis

The project depends on [MongoDB][] 3.2+, [ElasticSearch][] 2.4 and [Redis][]
(beware of the version, it will not work well if they are not respected).

Elasticsearch requires the [Analysis ICU][analysis-icu] plugin for your specific version.

The installation process is very specific to your operating system
and will depend on your configuration, join us on [Gitter][] if you have any issue.

On Debian, you need to add the appropriate apt repository:

    deb https://packages.elastic.co/elasticsearch/2.x/debian stable main

and install it like any other Debian package (You might need to enable Debian Backport repository)
The `plugin` command is located in the `/usr/share/elasticsearch/bin` directory.

For example, on Debian Jessie, you will have to perform (as root):

```shell
$ echo "deb https://packages.elastic.co/elasticsearch/2.x/debian stable main" \
    > /etc/apt/sources.list.d/elasticsearch.list
$ echo "deb http://http.debian.net/debian jessie-backports main contrib non-free" \
    > /etc/apt/sources.list.d/debian-backports.list
$ apt-get update
$ apt-get install elasticsearch
$ /usr/share/elasticsearch/bin/plugin install analysis-icu
$ service elasticsearch restart
```

If you are using [Homebrew][] (OSX):

```shell
$ brew install elasticsearch
$ /usr/local/Cellar/elasticsearch/2.4.1/libexec/bin/plugin install analysis-icu
```

[mongodb]: https://www.mongodb.org/
[elasticsearch]: https://www.elastic.co/products/elasticsearch
[redis]: http://redis.io/
[gitter]: https://gitter.im/opendatateam/udata
[homebrew]: http://brew.sh/
[python]: https://www.python.org/
[analysis-icu]: https://github.com/elastic/elasticsearch-analysis-icu
