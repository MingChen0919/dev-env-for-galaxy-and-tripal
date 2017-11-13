# Create temporary working directory

```
mkdir -p ~/Desktop/tripal-dev && cd ~/Desktop/tripal-dev
mkdir tripal_extensions && git clone https://github.com/tripal/tripal_analysis_expression.git tripal_extensions/tripal_analysis_expression
mkdir host_files
git clone https://github.com/tripal/tripal.git


```

# Launch Tripal site

```
docker run -it --rm -p 80:80 \
-v ~/Desktop/tripal-dev/tripal_extensions:/var/www/html/sites/all/modules/tripal_extensions \
-v ~/Desktop/tripal-dev/host_files:/var/www/html/sites/default/files/host_files \
-v ~/Desktop/tripal-dev/tripal:/var/www/html/sites/all/modules/tripal \
bcondon/docker_tripal3:withExpression /bin/bash
```
