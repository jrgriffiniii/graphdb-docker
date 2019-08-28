
# Building the image

## Downloading GraphDB

This needs to be downloaded from the following: URL

```
docker build -t jrgriffiniii/graphdb-free .
```

# Deploying the image
```
docker run --name 'graphdb' -p 7200:7200 -d -t jrgriffiniii/graphdb-free
```

# Creating a repository

_Ensure that one has cURL installed_

```
curl -X POST http://localhost:7200/rest/repositories\
     -H 'Content-Type: multipart/form-data'\
     -F "config=@repo-config.ttl"
```

# List the repositories

```
curl -G http://localhost:7200/rest/repositories\
     -H 'Accept: application/json'
```

_The server should respond with something similar to the following:_
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
