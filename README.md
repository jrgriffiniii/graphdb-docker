# GraphDB Server for Docker

GraphDB is a RDF graph store developed and maintained by Ontotext.  This
offers the free release of their server within a Docker container, along with a
basic repository configuration for usage with the Fedora Commons Repository.

## Primary Contacts

### Product Owner
[James Griffin](https://github.com/jrgriffiniii)

# Building the image

## Downloading GraphDB

This needs to be downloaded using the Ontotext request form located at: https://www.ontotext.com/products/graphdb/graphdb-free/
_Ontotext will send you an e-mail providing a link "Download as a stand-alone server".  Please use this to download the ZIP-compressed distribution._
Once this has been downloaded, please place it in the root directory path for
this repository.

## Building the image

```
docker build -t jrgriffiniii/graphdb:latest .
```

# Deploying the image
```
docker run --name 'graphdb' -p 7200:7200 -d -t jrgriffiniii/graphdb:latest
```

## Adding the default repository

### Install cURL
_macOS:_
```
brew install curl
```
_Ubuntu/Debian:_
```
apt-get install curl
```

## Creating a repository

_Ensure that one has cURL installed_

```
curl -X POST http://localhost:7200/rest/repositories\
     -H 'Content-Type: multipart/form-data'\
     -F "config=@repo-config.ttl"
```

## List the repositories

```
curl -G http://localhost:7200/rest/repositories\
     -H 'Accept: application/json'
```

_The server should respond with an entry similar to the following:_
```json
[
  {
    "id": "fcrepo",
    "title": "Fedora Commons Repository Resource Graphs",
    "uri": "http:\/\/localhost:7200\/repositories\/fcrepo",
    "externalUrl": "http:\/\/172.17.0.2:7200\/repositories\/fcrepo",
    "type": "free",
    "sesameType": "graphdb:FreeSailRepository",
    "location": "",
    "readable": true,
    "writable": true,
    "unsupported": false,
    "local": true
  }
]
```

# Releasing a new Version

## Commit the new version
```
docker commit -a'user@email.com' -m'Introduces my new changes' graphdb jrgriffiniii/graphdb:latest
```

For example, when releasing version 9.0.0 with an upgraded release of GraphDB
9.0.0 and with CORS disabled, the following was committed:
```
docker commit -a'jrgriffiniii@gmail.com' -m'Updating to release 9.0.0; Ensuring
that CORS is enabled for the server' graphdb
```

## Tag the new version
```
docker tag jrgriffiniii/graphdb:latest jrgriffiniii/graphdb:[VERSION]
```

## Push to the repository
```
docker push jrgriffiniii/graphdb:latest
docker push jrgriffiniii/graphdb:[VERSION]
```

## Update the documentation
- Publish any new updates on https://cloud.docker.com/repository/docker/jrgriffiniii/graphdb/general
- Publish the new release on https://github.com/jrgriffiniii/graphdb-docker

## ?

## Profit

# Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/jrgriffiniii/graphdb-docker/.
