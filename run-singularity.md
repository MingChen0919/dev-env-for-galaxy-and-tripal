# Singularity development

```
mkdir -p ~/Desktop/singularity-images && cd ~/Desktop/singularity-images
docker run -it \
  -v singularity-images:/home/singularity-images \
  mingchen0919/docker-singularity
```

# Run Singularity

Singularity can be installed on Mac OS with vagrant. Since I have Docker installed on my computer, I would like to try singularity within
a Docker ubuntu container.

Let's pull an ubuntu image and install singularity.
```
docker run -it ubuntu

# install singularity
apt-get update && \
    apt-get install \
    python \
    dh-autoreconf \
    build-essential
    
apt-get install -y git
git clone https://github.com/singularityware/singularity.git
cd singularity
./autogen.sh
./configure --prefix=/usr/local --sysconfdir=/etc
make
make install
```

# Build docker singularity image

I would like to build a Docker singularity image for later use.
```
docker commit [container ID] mingchen0919/docker-singularity
```



