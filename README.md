![Build and Test Status](https://github.com/hubot-friends/hubot-redis-brain/actions/workflows/ci-pipeline.yml/badge.svg)

# hubot-redis-brain

A hubot script to persist hubot's brain using Redis. This version is fork from the original [hubot-redis-brain](https://github.com/hubotio/hubot-redis-brain) that manages data via a JSON document.

This version utilizes Redis' Hash data structure to manage the data.

See [`scripts/RedisBrain.js`](scripts/RedisBrain.js) for full documentation.

## Installation

In hubot project repo, run:

`npm install @hubot-friends/hubot-redis-brain --save`

Then add **hubot-redis-brain** to your `external-scripts.json`:

```json
[
  "@hubot-friends/hubot-redis-brain"
]
```

## Configuration

`hubot-redis-brain` requires a Redis server to work. It uses the `REDIS_URL` environment variable for determining
where to connect to. The default is on localhost, port 6379 (ie the redis default).

Note: you can use the following command to start a local instance of Redis using Docker:

```sh
docker run --rm -p 6379:6379 -d --name hubot-redis -v $(pwd)/redis-data:/data redis redis-server --appendonly yes"
```

The following attributes can be set using the `REDIS_URL`

* authentication
* hostname
* port
* key prefix

For example, `export REDIS_URL=redis://:password@192.168.0.1:16379/prefix` would
authenticate with `password`, connecting to `192.168.0.1` on port `16379`, and store
data using the `prefix:storage` key.

For a UNIX domain socket, `export REDIS_URL=redis://:password@/var/run/redis.sock?prefix` would authenticate with `password`, connecting to `/var/run/redis.sock`, and store data using the `prefix:storage` key.

### Installing your own

If you need to install and
run your own, most package managers have a package for redis:

* Mac OS X with homebrew: `brew install redis`
* Ubuntu/Debian with apt: `apt-get install redis-server`
* Compile from source: http://redis.io/topics/quickstart

### Redis Twemproxy

If you are using [Twemproxy](https://github.com/twitter/twemproxy) to cluster redis,
you need to turn off the redis ready check which uses the unsupported INFO cmd.

`REDIS_NO_CHECK = 1`
