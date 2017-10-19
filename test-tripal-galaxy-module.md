# Working directory

First of all, always create a temporary working directory. Whenever starting working on the project, pull the code
from github repositories and place them into this working directory. When stopping working, push the code to github
and remove everything from the local computer.


``` 
cd ~/Desktop
mkdir test-tripal-galaxy
cd test-tripal-galaxy
```

# Docker container network

This project needs two containers running and talking to each other. One container is
for a Tripal site and the other is for a Galaxy instance.


# [Create a docker network](https://docs.docker.com/engine/userguide/networking/#bridge-networks)

```
docker network create --driver bridge tripal_galaxy_nw
```


## Launch containers on the created network.

* Launch Galaxy instance

```
# create a directory to mount to the docker container's tool directory so that I can update or debug tools from the host machine
mkdir shed_tools
 
docker run -it --rm --network=tripal_galaxy_nw --name=galaxy_instance \
        -p 8080:80 -p 8021:21 -p 8800:8800 \
        -v $(pwd)/shed_tools:/export/shed_tools \ 
		-e "ENABLE_TTS_INSTALL=True" \
	    -e "GALAXY_CONFIG_ADMIN_USERS=example@gmail.com" \
	    bgruening/galaxy-stable:17.01 /bin/bash
```

* Launch Tripal site

``` 
sudo docker run -it --rm --network=tripal_galaxy_nw --name=tripal_site \
        -p 8090:80 mingchen0919/docker-tripal-v3 /bin/bash
```

## Obtain container IP address

``` 
docker network inspect tripal_galaxy_nw
```

The command above will output a JSON array. Within the `containers` filed, all the API address info will show up for each container.


The **Tripal Galaxy** module uses URL not IP address to connect to a Galaxy instance. See the screenshot below:

![tripal galaxy connection](images/tripal_galaxy_connect_to_galaxy.png)

