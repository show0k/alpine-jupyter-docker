# Poppy docker
Provide a docker image for runing a Jupyter notebook with Poppy libraries.

```
docker run -i -t -p 8888:8888 -v \
<path to your ipython notebooks on host>:/home/condauser/notebooks show0k/poppy-docker \
/home/condauser/anaconda3/bin/ipython notebook
```

