# Create temporary working directory

``` 
cd ~/Desktop
mkdir galaxy-tool-generator
cd galaxy-tool-generator
```

# Clone repositories

```
mkdir galaxy_tools 
mkdir custom
git clone https://github.com/MingChen0919/galaxy_tool_generator.git custom/galaxy_tool_generator
git clone https://github.com/MingChen0919/galaxy_tool_generator_ui.git custom/galaxy_tool_generator_ui
```

# Docker container network

This project needs two containers running and talking to each other. One container is
for a Tripal site and the other is for a Galaxy instance.


# [Create a docker network](https://docs.docker.com/engine/userguide/networking/#bridge-networks)

```
docker network create --driver bridge galaxy_tool_generator_nw
```

## Launch containers on the created network.

### Launch Galaxy instance

```
# create a directory to mount to the docker container's tool directory so that I can update or debug tools from the host machine
mkdir shed_tools
 
docker run -it --rm --network=galaxy_tool_generator_nw --name=galaxy_instance \
        -p 8080:80 -p 8021:21 -p 8800:8800 \
        -v $(pwd)/shed_tools:/export/shed_tools \
        -e "ENABLE_TTS_INSTALL=True" \
        -e "GALAXY_CONFIG_ADMIN_USERS=example@gmail.com" \
        bgruening/galaxy-stable:17.01 /bin/bash
```


### Launch Tripal site

``` 
cd galaxy-tool-generator
docker run -it -p 8090:80 --rm \
            -v $(pwd)/galaxy_tools:/var/www/html/sites/default/files/galaxy_tools \
            -v $(pwd)/custom:/var/www/html/sites/all/modules/custom \
            -v ~/.planemo.yml:/root/.planemo.yml \
            mingchen0919/docker-galaxy-tool-generator '/bin/bash'
```            
   
* Pull updates for dependency library blend4php

```
cd /var/www/html/sites/all/libraries/blend4php
git pull
```

* Within the tripal site container, run the following command
```
drush en -y galaxy_tool_generator galaxy_tool_generator_ui
```
