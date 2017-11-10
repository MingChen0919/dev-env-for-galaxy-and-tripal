# Develop Drupal/Tripal modules

**The internal apache needs to be stoped if we want to map the container port `80` to the host port `80`**

```
sudo apachectl stop
```

```
# create a directory to host custom modules
mkdir -p ~/Desktop/custom && cd ~/Desktop/custom

# launch a Tripal site
docker run --rm -it -p 80:80 \
  -v ~/Desktop/custom:/var/www/html/sites/all/modules/custom \
  mingchen0919/docker-tripal-v3 /bin/bash
```

# Account names and passwords for Tripal 3 site

* Tripal site admin username: `admin`
* Tripal site password: `P@55w0rd`
* Postgres database name: `tripal_db`
* Postgres database username: `tripal`
* Postgres database password: `tripal_db_passwd`
