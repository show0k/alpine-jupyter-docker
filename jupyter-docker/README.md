# Poppy docker
Provide a docker image for runing a Jupyter notebook with Poppy libraries.


```
docker run -d -p 8888:8888 -p 6969:6969 -p 8080:8080 show0k/poppy-docker start-notebook.sh
```


To start this image in a spawner tmpnb service, you must do:

```bash
sudo docker pull show0k/poppy-docker
export TOKEN=$( head -c 30 /dev/urandom | xxd -p )

sudo docker run --net=host -d -e CONFIGPROXY_AUTH_TOKEN=$TOKEN --name=proxy jupyter/configurable-http-proxy --default-target http://127.0.0.1:9999

sudo docker run --net=host -d -e CONFIGPROXY_AUTH_TOKEN=$TOKEN \
           -v /var/run/docker.sock:/docker.sock \
           jupyter/tmpnb python orchestrate.py --image="show0k/poppy-docker" \
           --command="start-notebook.sh \"--NotebookApp.base_url={base_path} --NotebookApp.allow_origin='*' --port={port}\""
```

