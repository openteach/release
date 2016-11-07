# OpenTeach releases
This repository contains deployment notes and releases

We assume the user is familiar with, and have following installed:

* docker
* docker-machine
* docker-compose

# Digital ocean

1. Create a VM with docker-machine

```
docker-machine create \
--driver=digitalocean \
--digitalocean-access-token=[access token] \
--digitalocean-size=512mb \
--digitalocean-region=fra1 \
--digitalocean-private-networking=true \
--digitalocean-image=ubuntu-16-04-x64 \
openteach
```


# Create a release
If you want to release cutting edge from the main repository, you can create a
release:

1. `meteor build --architecture=os.linux.x86_64 ./`
2. move the newly created file, `openteach.tar.gz`, to a public location on
   the web
3. Update the docker compose file
4. Do a compose up.
