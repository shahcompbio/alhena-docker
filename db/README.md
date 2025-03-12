


## Running Alhena
Bringing up the containers:
```
docker-compose -f docker-compose.yml up -d
```
Bringing them down:
```
docker-compose -f docker-compose.yml down
```

## Cert Creation
Runs off the `instances.yml` and creates cert for each node. 

When new nodes are added, they must be added to `instaces.yaml` and cert creation must be run.

Command
```
docker-compose -f create-certs.yml up
```

## New Mount Permissions
To avoid running into `AccessDeniedException` issues, permissions must be set as follows:
```
sudo chown -R 1000:root /path/to/mount
```
The above is only relevant when adding new nodes.


## Status of Nodes
```
curl -u "USER:PASS" -k https://plvicosspecdat1:9200/_cat/allocation\?pretty\=true
```

To get details on the columns run:
```
curl -u "USER:PASS" -k https://plvicosspecdat1:9200/_cat/allocation\?help
```

Note: if there are special character like ! in your password escape with backslash \.


## Server Restarts
After a server patch we had problems bringing up the containers with the error
"[1]: max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]" in es01 container.

To fix this we ran the following command
sysctl -w vm.max_map_count=262144

After bringing up the containers you need to wait around 10 minutes for things to start working smoothly again.
