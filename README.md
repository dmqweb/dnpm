# ‼️ ‼️ ‼️ ‼️ DEPRECATED, please use https://github.com/dnpm/dnpmcore instead ‼️ ‼️ ‼️ ‼️


------

dnpmjs.org
=======

(https://github.com/dnpm/dnpmjs.org/actions/workflows/nodejs.yml)
[![Test coverage][codecov-image]][codecov-url]
[![Known Vulnerabilities][snyk-image]][snyk-url]
[![npm download][download-image]][download-url]
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fdnpm%2Fdnpmjs.org.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2Fdnpm%2Fdnpmjs.org?ref=badge_shield)

[npm-image]: http://dnpmjs.org/badge/v/dnpmjs.org.svg?style=flat-square
[npm-url]: http://dnpmjs.org/package/dnpmjs.org
[codecov-image]: https://codecov.io/gh/dnpm/dnpmjs.org/branch/master/graph/badge.svg
[codecov-url]: https://codecov.io/gh/dnpm/dnpmjs.org
[snyk-image]: https://snyk.io/test/npm/dnpmjs.org/badge.svg?style=flat-square
[snyk-url]: https://snyk.io/test/npm/dnpmjs.org
[download-image]: https://img.shields.io/npm/dm/dnpmjs.org.svg?style=flat-square
[download-url]: https://npmjs.org/package/dnpmjs.org


## Description

Private npm registry and web for Enterprise, base on [koa](http://koajs.com/),
MySQL and [Simple Store Service](https://github.com/dnpm/dnpmjs.org/wiki/NFS-Guide).

Our goal is to provide a low cost maintenance, easy to use, and easy to scale solution for private npm.

## What can you do with `dnpmjs.org`?

* Build a private npm for your own enterprise. ([alibaba](http://www.alibaba.com/) is using `dnpmjs.org` now)
* Build a npm mirror. (we use it to build a mirror in China: [https://npmmirror.com/](https://npmmirror.com/))
* Use the private npm service provided by Alibaba Cloud DevOps which build with npm. [https://packages.aliyun.com/](https://packages.aliyun.com/?channel=pd_dnpm_github)

## Features

* **Support "scoped" packages**: [npm/npm#5239](https://github.com/npm/npm/issues/5239)
* **Support [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing)**
* **Simple to deploy**: only need `mysql` and a [simple store system](https://github.com/dnpm/dnpmjs.org/wiki/NFS-Guide).
* **Low cost and easy maintenance**: `package.json` info can store in MySQL, MariaDB, SQLite or PostgreSQL.
tarball(tgz file) can store in Amazon S3 or other object storage service.
* **Automatic synchronization**: automatically sync from any registry specified. support two sync modes:
  - Sync all modules from upstream
  - Only sync the modules after first access.
* **Manual synchronization**: automatic synchronization may has little delay. you can sync manually on web page.
* **Customized client**: we provide a client [dnpm](https://github.com/dnpm/dnpm)
to extend `npm` with more features(`sync` command, [gzip](https://github.com/npm/npm-registry-client/pull/40) support).
And it is easy to wrap for your own registry which build with `dnpmjs.org`.
* **Compatible with npm client**: you can use the official npm client with `dnpmjs.org`.
you only need to change the registry in client config.
* **Support http_proxy**: if you're behind a firewall, you can provide a http proxy for dnpmjs.org.

## Docs

* [How to deploy](https://github.com/dnpm/dnpmjs.org/wiki/Deploy)
* dnpm client: [dnpm](https://github.com/dnpm/dnpm), `npm install -g dnpm`
* [Sync packages through `http_proxy`](https://github.com/dnpm/dnpmjs.org/wiki/Sync-packages-through-http_proxy)
* [Migrating from 1.x to 2.x](https://github.com/dnpm/dnpmjs.org/wiki/Migrating-from-1.x-to-2.x)
* [New features in 2.x](https://github.com/dnpm/dnpmjs.org/wiki/New-features-in-2.x).
* [wiki](https://github.com/dnpm/dnpmjs.org/wiki)

## Develop on your local machine

### Dependencies

* [node](http://nodejs.org) >= 8.0.0
* Databases: only required one type
  * [sqlite3](https://npmmirror.com/package/sqlite3) >= 3.0.2, we use `sqlite3` by default
  * [MySQL](http://dev.mysql.com/downloads/) >= 5.6.16, include `mysqld` and `mysql cli`. I test on `mysql@5.6.16`.
  * MariaDB
  * PostgreSQL

### Clone code and run test

```bash
# clone from git
$ git clone https://github.com/dnpm/dnpmjs.org.git

# install dependencies
$ make install

# test
$ make test

# coverage
$ make test-cov

# update dependencies
$ make autod

# start server with development mode
$ make dev
```

### Dockerized dnpmjs.org Installation Guide

dnpmjs.org shipped with a simple but pragmatic Docker Compose configuration.With the configuration, you can set up a MySQL backend dnpmjs.org instance by executing just one command on Docker installed environment.

#### Preparation

* [Install Docker](https://www.docker.com/community-edition)
* [Install Docker Compose](https://docs.docker.com/compose/install/) (Docker for Mac, Docker for Windows include Docker Compose, so most Mac and Windows users do not need to install Docker Compose separately)
* (Optional) Speed up Docker images downloading by setting up [Docker images download accelerator](https://yq.aliyun.com/articles/29941)


#### Dockerized dnpmjs.org control command

Make sure your current working directory is the root of this GitHub repository.

##### Run dockerized dnpmjs.org

```bash
 $docker-compose up
 ```

This command will build a Docker image using the current code of repository. Then set up a dockerized MySQL instance with data initialized. After Docker container running, you can access your dnpmjs.org web portal at http://127.0.0.1:7002 and npm register at http://127.0.0.1:7001.

#### Run dnpmjs.org in the backend

```bash
$docker-compose up -d
```

#### Rebuild dnpmjs.org Docker image

```bash
$docker-compose build
```

#### Remove current dockerized dnpmjs.org instance

The current configuration set 2 named Docker Volume for your persistent data. If you haven't change the repository directory name, them will be "dnpmjsorg_dnpm-files-volume" & "dnpmjsorg_dnpm-db-volume".

Be Careful, the following commands will remove them.

```bash
$docker-compose rm
$docker volume rm dnpmjsorg_dnpm-files-volume
$docker volume rm dnpmjsorg_dnpm-db-volume
```

You can get more information about your data volumes using the below commands:

```bash
$docker volume ls  // list all of your Docker volume
$docker volume inspect dnpmjsorg_dnpm-files-volume
$docker volume inspect dnpmjsorg_dnpm-db-volume
```

## How to contribute

* Clone the project
* Checkout a new branch
* Add new features or fix bugs in the new branch
* Make a pull request and we will review it ASAP

Tips: make sure your code is following the [node-style-guide](https://github.com/felixge/node-style-guide).

## Sponsors

- [![阿里云](https://static.aliyun.com/images/www-summerwind/logo.gif)](http://click.aliyun.com/m/4288/) [![阿里云云效](https://img.alicdn.com/tfs/TB116yt3fb2gK0jSZK9XXaEgFXa-106-20.png)](https://devops.aliyun.com/?channel=pd_dnpm_github) (2016.2 - now)

## License

[MIT](LICENSE.txt)

<!-- GITCONTRIBUTOR_START -->

