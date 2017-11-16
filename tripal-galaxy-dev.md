# Tripal Galaxy module development

```
mkdir -p ~/Desktop/tripal-galaxy-dev && cd ~/Desktop/tripal-galaxy-dev


docker run -it --rm --network=tripal_galaxy_nw --name=tripal_site \
        -v ~/Desktop/tripal-galaxy-dev/tripal:/var/www/html/sites/all/modules/tripal \
        -v ~/Desktop/tripal-galaxy-dev/tripal_galaxy:/var/www/html/sites/all/modules/tripal_galaxy \
        -v ~/Desktop/tripal-galaxy-dev/blend4php:/var/www/html/sites/all/libraries/blend4php \
        -p 80:80 mingchen0919/docker-tripal-v3 /bin/bash
        
cd ~/Desktop/tripal-galaxy-dev
git clone https://github.com/tripal/tripal.git
git clone https://github.com/galaxyproject/blend4php.git
git clone https://github.com/statonlab/tripal_galaxy.git
```
