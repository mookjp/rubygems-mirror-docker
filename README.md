rubygems-mirror-docker
===

Docker image of [rubygems-mirror](https://github.com/rubygems/rubygems-mirror).

## Usage

Before starting gem server, it needs to fetch packages from rubygems to mirror directory.
Create data container first to make gem packages portable.

```
docker create --name gems-data -v /data/rubygems busybox
# Fetch packages to data only container
docker run -d --volumes-from gems-data rubygems-mirror gem mirror
```

then run server as your mirror.

```
docker run -d --volumes-from gems-data -p 9292 rubygems-mirror
```

## Set your mirror

Set your rubygems mirror by following:

* http://bundler.io/v1.10/bundle_config.html

```
bundle config mirror.http://rubygems.org http://your-mirror-address:9292
```

* http://guides.rubygems.org/run-your-own-gem-server/#using-gems-from-your-server

```
gem sources --add http://your-mirror-address:9292
```
