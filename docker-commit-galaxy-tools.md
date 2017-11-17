# Docker commit Galaxy tools

Run an empty Galaxy instance, install tools through Galaxy interface and build new image with `docker commit`.

```
docker run -it --name=galaxy_instance \
    -p 80:80 -p 8021:21 -p 8800:8800 \
    -e "ENABLE_TTS_INSTALL=True" \
    -e "GALAXY_CONFIG_ADMIN_USERS=example@gmail.com" \
    bgruening/galaxy-stable:17.01 /bin/bash
```
