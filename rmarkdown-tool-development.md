# Create temporary working directory

``` 
cd ~/Desktop
mkdir rmarkdown-tool-dev
cd rmarkdown-tool-dev
```

# Clone repository to local

``` 
git clone https://github.com/statonlab/docker-GRReport.git

mkdir shed_tools
```

# Launch Galaxy container

``` 
sudo docker run -it --rm -p 8080:80 -p 8021:21 -p 8022:22  \
    -v $(pwd)/shed_tools:/export/shed_tools \
    -e "ENABLE_TTS_INSTALL=True" \
    -e "GALAXY_CONFIG_ADMIN_USERS=example@gmail.com" \
    bgruening/galaxy-stable:17.01 /bin/bash
```

# Publish to toolshed/testtoolshed

## Toolshed

* Create a repository

```
planemo shed_create --shed_target toolshed
```

* Update repository

```
planemo shed_update --check_diff --shed_target toolshed
```
