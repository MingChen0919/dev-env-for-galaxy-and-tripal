# Develop Drupal/Tripal modules

```
# create a directory to host custom modules
mkdir -p ~/Desktop/custom && cd ~/Desktop/custom

# launch a Tripal site
docker run --rm -it -p 8080:80 \
  -v ~/Desktop/custom:/var/www/html/sites/all/modules \
  mingchen0919/docker-tripal-v3 /bin/bash
```
