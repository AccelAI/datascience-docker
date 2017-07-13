Accel.ai Basic Deep Learning & AI Docker Image 
======================

Docker container with basic Python data science, Deep Learning, and AI tools:
  - graphviz 
  - jupyter 
  - keras 
  - pandas 
  - pytorch 
  - scipy (numpy & matplotlib)
  - scikit-learn 
  - seaborn 
  - tensorflow 
  - theano 

 This is an image adapted from one created by [wise.io](http://wise.io) datascience [git repo](https://github.com/wiseio/datascience-docker),
 with the underlying python distribution coming from [Continuum/Miniconda3](http://continuum.io)

## Getting up and running

1)  Install Docker [Docker for Mac](https://www.docker.com/docker-mac) [Docker for Windows](https://www.docker.com/docker-windows)
2)  Start Docker 
3)  Run the following commands in the terminal/command prompt to start the container:
    `docker pull accelai/julyworkshop`
    `docker run -it accelai/julyworkshop /bin/bash`
    
    *If you would rather have a Jupyter Notebook interface, run the following command in the terminal/command prompt:*

    `docker run -it -p 8888:8888 accelai:julyworkshop /bin/bash -c "/opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser --allow-root"`

    This will produce a message in the terminal about where Jupyter is running.  You can then view the Jupyter Notebook by opening that URL in your browser.


## Using the Container Directly##

Once you're running the container, you can get a terminal window inside if needed:

```
docker exec -it <container_name> bash
```

Here you can add new functionality if you need it. E.g.,

```
apt-get package-name
conda install <package name>
pip install requirements.txt

...
```

Note that this will only add functionality into the container itself, not the image. If you want to use this new functionality, you'll want to add it to the image by hacking the Dockerfile.

## Hacking on the Dockerfile

Clone the repository from whence this image was made, make changes then build the container:

```
git clone <repo name>
cd datascience-docker
docker build -t  datascience-base .
docker run -d -p 80:8888 datascience-base
```

## Use your own certificate
This image looks for `/key.pem`. If it doesn't exist a self signed certificate will be made. If you would like to use your own certificate, concatenate your private and public key along with possible intermediate certificates in a pem file. The order should be (top to bottom): key, certificate, intermediate certificate.

Example:

```
cat hostname.key hostname.pub.cert intermidiate.cert > hostname.pem
```

Then you would mount this file to the docker container:

```
docker run -v /path/to/hostname.pem:/key.pem -d -p 443:8888 -e "PASSWORD=pass" wiseio/datascience-base
```

## Using HTTPS
This docker image by default runs Jupyter in HTTP.  If you'd like to run this in HTTPS,
you can use the `USE_HTTP` environment variable.  Setting it to zero enables HTTPS.

Example:

```
docker run -d -p 443:8888 -e "PASSWORD=$IPYTHON_PASSWORD" -e "USE_HTTP=0" accelai/datascience-base

You'll then connect via https://<ip>`
```