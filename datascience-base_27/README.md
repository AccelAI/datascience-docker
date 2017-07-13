# Python 2.7.11 Deep Learning & AI  Image

This is an image adapted from one created by [wise.io](http://wise.io) datascience [git repo](https://github.com/wiseio/datascience-docker), with the underlying python distribution coming from [Continuum/Miniconda3](http://continuum.io).  We've pre-installed the following to get you started:

  - _graphviz_ 
  - _jupyter_ 
  - _keras_ 
  - _pandas_ 
  - _pytorch_ 
  - _scipy (numpy & matplotlib)_
  - _scikit-learn_ 
  - _seaborn_ 
  - _tensorflow_ 
  - _theano_ 


## Getting up and running

### Install Docker

 - For those running a **_linux_** distro, you should be able to `apt-get/yum docker`. 
 - For those on **_OS X_**, you'll need to check out [Docker for Mac](https://www.docker.com/docker-mac) || [Docker Toolbox for Mac (Legacy)](https://docs.docker.com/toolbox/toolbox_install_mac/) 
 - For those on **_Windows_**, you'll want to go to [Docker for Windows](https://www.docker.com/docker-windows) || [Docker for Windows 7 (Legacy)](https://docs.docker.com/toolbox/toolbox_install_windows/)

### Pull the Docker Image You Need

This Miniconda2-based image is hosted at the **Docker Hub**. You can grab it with:

**Python 2.6=7.11:**    ```docker pull accelai/datascience-base_27```

### Start the container via terminal/command prompt:

   ```docker pull accelai/datascience-docker_27```
   ```docker run -it accelai/datascience-docker_27/bin/bash```
    
### Alternatively, start a Jupyter Notebook interface:

   ```
docker run -it -p 8888:8888 accelai/datascience-docker_27 /bin/bash -c "/opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser --allow-root"
```

## Using the Container Directly

Once you're running the container, you can get a terminal window inside if needed:

```docker exec -it <container_name> bash```

Here you can add new functionality if you need it. **_E.g._**, 

```

apt-get package-name
conda install <package name>
pip install requirements.txt

```

_**Note**:  this will only add functionality into the container itself, not the image. If you want to use this new functionality, you'll want to add it to the image by hacking the **Dockerfile**._


## Hacking on the Dockerfile

Clone the repository from whence this image was made, make changes then build the container:

```
git clone https://github.com/AccelAI/datascience-docker_27/
cd datascience-docker_27
docker build -t  datascience-base_27 .
docker run -d -p 80:8888 datascience-base_27
```

## Use your own certificate
This image looks for `/key.pem`. If it doesn't exist a self signed certificate will be made. If you would like to use your own certificate, concatenate your private and public key along with possible intermediate certificates in a pem file. The order should be (top to bottom): key, certificate, intermediate certificate.

**Example:**

```cat hostname.key hostname.pub.cert intermidiate.cert > hostname.pem```

Then you would mount this file to the docker container:

```
docker run -v /path/to/hostname.pem:/key.pem -d -p 443:8888 -e "PASSWORD=pass" accelai/datascience-base_27
```

## Using HTTPS
This docker image by default runs Jupyter in HTTP.  If you'd like to run this in HTTPS,
you can use the `USE_HTTP` environment variable.  **Setting it to zero enables HTTPS**.

**Example:**

```
docker run -d -p 443:8888 -e "PASSWORD=$IPYTHON_PASSWORD" -e "USE_HTTP=0" accelai/datascience-base_27

You'll then connect via https://<ip>`
```
