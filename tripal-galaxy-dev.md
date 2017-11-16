# Tripal Galaxy module development

```
mkdir -p ~/Desktop/tripal-galaxy-dev && cd ~/Desktop/tripal-galaxy-dev
        
git clone https://github.com/tripal/tripal.git
git clone https://github.com/galaxyproject/blend4php.git
git clone https://github.com/statonlab/tripal_galaxy.git

docker run -it --name=tripal-galaxy-dev \
        -v ~/Desktop/tripal-galaxy-dev/tripal:/var/www/html/sites/all/modules/tripal \
        -v ~/Desktop/tripal-galaxy-dev/tripal_galaxy:/var/www/html/sites/all/modules/tripal_galaxy \
        -v ~/Desktop/tripal-galaxy-dev/blend4php:/var/www/html/sites/all/libraries/blend4php \
        -p 80:80 mingchen0919/docker-tripal-v3 /bin/bash

```


# Edit `settings.php` file

```
# copy and paste the following content to the bottom of settings.php
$conf['drupal_http_request_fails'] = FALSE;
$conf['theme_debug'] = TRUE; ## uncomment this line in settings.php
error_reporting(-1);  // Have PHP complain about absolutely everything
$conf['error_level'] = 2;  // Show all messages on your screen, 2 = ERROR_REPORTING_DISPLAY_ALL.
ini_set('display_errors', TRUE);  // These lines just give you content on WSOD pages.
ini_set('display_startup_errors', TRUE);
```

# Remove container

```
docker rm tripal-galaxy-dev
```
