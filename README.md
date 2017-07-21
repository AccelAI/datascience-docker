# datascience-docker

Containers and material for the **Accel.ai Demystifying Deep Learning and AI Workshop** _July 21st - 23rd, 2017._



## Introduction ##

If you haven't used Docker before, a good place to start is the [Docker User Guide](https://docs.docker.com/userguide/).

- For those running a **_linux_** distro, you should be able to `apt-get/yum docker`. 
- For those on **_OS X_**, you'll need to check out [Docker for Mac](https://www.docker.com/docker-mac) || [*Docker Toolbox for Mac (Legacy)*](https://docs.docker.com/toolbox/toolbox_install_mac/) 
- For those on **_Windows_**, you'll want to go to [Docker for Windows](https://www.docker.com/docker-windows) || [*Docker for Windows 7 (Legacy)*](https://docs.docker.com/toolbox/toolbox_install_windows/)

## Getting Started ##

The Miniconda3-based and Miniconda2-based images are hosted at the **Docker Hub**. You can grab them with:


**Python 3.6.1**
```
docker pull accelai/datascience-docker
```

**Python 2.7.11**

```
docker pull accelai/datascience-docker_27
```

The **README.md** in `datascience-base/` and `datascience-base_27`give an overview of how to use those images to run containers locally, and start a Jupyter server for Notebooks.


