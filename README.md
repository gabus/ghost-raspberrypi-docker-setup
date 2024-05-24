# ghost-raspberrypi-docker-setup


### Ghost Docker image 
```yaml
version: '3.1'

services:

  ghost:
    image: ghost:5
    restart: always
    ports:
      - 8090:2368
    environment:
      # keep https if you're planing to use ssl
      url: https://your-blog.co.uk
    
      # see https://ghost.org/docs/config/#configuration-options
      database__client: mysql
      database__connection__host: db
      database__connection__user: root
      database__connection__password: gsttHRAhaf5546
      database__connection__database: ghost
      
      # contrary to the default mentioned in the linked documentation, this image defaults to NODE_ENV=production (so development mode needs to be explicitly specified if desired)
      #NODE_ENV: development
    volumes:
      - ghost:/var/lib/ghost/content

  db:
    image: mysql:8
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: gsttHRAhaf5546
    volumes:
      - db:/var/lib/mysql

volumes:
  ghost:
  db:
 ```


### Useful commands
```bash
ssh gabe@192.168.1.175

sudo docker exec -it e3b05925e21b /bin/bash
su node

# install nano (ghost image doesn't have it by default)
apt-get update
apt-get install nano


# copy all files from docker container into local environment
sudo docker cp e3b05925e21b:/var/lib/ghost/content ./ghost-content

# copy files from ssh instance to local environment
scp -r gabe@192.168.1.175:/home/gabe/ghost-content ./ghost-content-files

# show docker processes in full length
docker ps --no-trunc
```
