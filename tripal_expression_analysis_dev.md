# Create temporary working directory

```
mkdir -p ~/Desktop/custom && cd ~/Desktop/custom
git clone https://github.com/tripal/tripal_analysis_expression.git
```

# Launch Tripal site

```
docker run -it -p 80:80 --rm \
            -v $(pwd)/custom:/var/www/html/sites/all/modules/custom \
            bcondon/docker_tripal3 '/bin/bash'
```
