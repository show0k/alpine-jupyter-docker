[![](https://images.microbadger.com/badges/image/show0k/alpine-miniconda.svg)](https://hub.docker.com/r/show0k/alpine-minimal/)
# Alpine Miniconda

Safe Miniconda install in an Alpine Linux container.
This image intend to be used as a base image, smaller than the official Continiuum image, based on Ubuntu.

The official Miniconda image [weigth 158MB](https://microbadger.com/images/continuumio/miniconda) and this one [only 57MB](https://microbadger.com/images/show0k/alpine-miniconda).


A special user is create with uid 1000 and can be use with any public user without security breach.


# Usage

You can download and run this image with these commands:

```
docker pull show0k/alpine-miniconda
docker run -i -t show0k/alpine-miniconda /bin/bash
```

If you need Jupyter notebook, another image based on Alpine is built my myself [here](https://github.com/show0k/alpine-jupyter-docker/tree/master/alpine-minimal-notebook).
