# Create temporary working directory

``` 
mkdir -p ~/Desktop/galaxy-tool-generator-dev && cd ~/Desktop/galaxy-tool-generator-dev
git clone https://github.com/MingChen0919/galaxy_tool_generator.git
git clone https://github.com/MingChen0919/galaxy_tool_generator_ui.git
git clone https://github.com/galaxyproject/blend4php.git
```

# Docker container network

This project needs two containers running and talking to each other. One container is
for a Tripal site and the other is for a Galaxy instance.


# [Create a docker network](https://docs.docker.com/engine/userguide/networking/#bridge-networks)

```
docker network create --driver bridge galaxy_tool_generator_nw
```

## Launch containers within the created network.

### Launch Tripal site

``` 
docker run -it -p 8090:80 --rm --network=galaxy_tool_generator_nw \
            -v $(pwd)/galaxy_tools:/var/www/html/sites/default/files/galaxy_tools \
            -v $(pwd)/galaxy_tool_generator:/var/www/html/sites/all/modules/galaxy_tool_generator \
            -v $(pwd)/galaxy_tool_generator_ui:/var/www/html/sites/all/modules/galaxy_tool_generator_ui \
            -v $(pwd/blend4php):/var/www/html/sites/all/libraries/blend4php \
            mingchen0919/docker-galaxy-tool-generator '/bin/bash'
            
# elasticsearch is not needed, so stop elasticsearch
service elasticsearch_node-01 stop
service elasticsearch_node-02 stop
```            


* Within the tripal site container, run the following command
```
drush en -y galaxy_tool_generator galaxy_tool_generator_ui
```


### Launch Galaxy instance

```
# create a directory to mount to the docker container's tool directory so that I can update or debug tools from the host machine
mkdir shed_tools
 
docker run -it --rm --network=galaxy_tool_generator_nw --name=galaxy_instance \
        -p 8080:80 -p 8021:21 -p 8022:22 \
        -v $(pwd)/shed_tools:/export/shed_tools \
        -e "ENABLE_TTS_INSTALL=True" \
        -e "GALAXY_CONFIG_ADMIN_USERS=example@gmail.com" \
        bgruening/galaxy-stable:17.01 /bin/bash
```



