# kontena-rocks

A local Kontena setup on steroids with real SSL cert and domain (.kontena.rocks) with SECURE registry.

```
bin/krocks install
krocks master create
[GRID_TRUSTED_SUBNET=192.168.0.0/16] krocks grid create [rocks]
[GRID_NAME=rocks] [GRID_NODE_MEMORY=1024] [GRID_INSTANCES=1] [GRID_IP_START=192.168.66.101] krocks node create
```

```
krocks node logs
krocks node logs 1
```

## demo

```
curl https://gist.githubusercontent.com/matti/ASK_ME_ON_KONTENA_SLACK_TO_GET_THIS/wildcard_kontena_rocks.pem | kontena vault update --upsert SSL_STAR_kontena_rocks

kontena stack install kontena/ingress-lb

> Affinity : label!=no-ingress-lb
> Pick SSL cert(s) from Vault SSL_STAR_kontena_rocks
...

kontena stack install matti/registry

> Enable htpasswd : No
> Enter KONTENA_LB_VIRTUAL_HOSTS : registry.kontena.rocks
> Pick a loadbalancer ingress-lb/lb
...

docker pull alpine:3.5
docker tag alpine:3.5 registry.kontena.rocks/alpine:3.5
docker push registry.kontena.rocks/alpine:3.5
```
