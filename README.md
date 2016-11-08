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
2. Use the new machine: `eval $(docker-machine env openteach)`
3. create docker-compose.yml from following template:
   ```
   openteach:
     image: kadirahq/meteord:base
     restart: always
     ports:
      + "80:80"
     links:
      + mongo
     environment:
      + MONGO_URL=mongodb://mongo/meteor-db
      + ROOT_URL=http://[YOUR DOMAIN]
      + BUNDLE_URL=https://raw.githubusercontent.com/openteach/release/master/releases/[RELEASE].tar.gz
      + METEOR_SETTINGS=[CONTENT OF SETTINGS.JSON]
   mongo:
     image: mongo:latest
   ```
4. Setup by issuing `docker-compose up -d`

__Settings.json:__ remove all white space characters before inserting the
string.

# Create a release
If you want to release cutting edge from the main repository, you can create a
release:

1. Run `meteor build --architecture=os.linux.x86_64 ./` in the library
2. Move the newly created file, `openteach.tar.gz`, to a public location on
   the web
3. Update the docker compose file
4. Do a `compose up -d`.
