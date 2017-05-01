### Docker In Windows Bash

Unfortunately, you can't run docker in Windows bash today. When you try to run docker in the bash subsystem you get an error like:

```
Client:
 Version:      17.03.1-ce
 API version:  1.27
 Go version:   go1.7.5
 Git commit:   c6d412e
 Built:        Mon Mar 27 17:10:36 2017
 OS/Arch:      linux/amd64

Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
```

That error may be quite puzzling, especially if you have [Docker for Windows](https://docs.docker.com/docker-for-windows/) already running on your machine. 

You can, however, use the docker client in bash to connect to the docker engine running in Windows on the same machine.

Sounds backwards, but it's true. How? Easy:

1. Launch a [bash window](https://msdn.microsoft.com/en-us/commandline/wsl/about)
2. Follow installation steps for [Docker on Ubuntu](https://docs.docker.com/engine/installation/linux/ubuntu/#install-using-the-repository) - since Windows subsystem is based on Ubuntu
3. Connect to the docker daemon using tcp instead of the linux socket or a windows pipe. Either add a -H pararmeter when you invoke docker

```
$ docker -H tcp://localhost version
Client:
 Version:      17.03.1-ce
 API version:  1.27
 Go version:   go1.7.5
 Git commit:   c6d412e
 Built:        Mon Mar 27 17:10:36 2017
 OS/Arch:      linux/amd64

Server:
 Version:      17.03.1-ce
 API version:  1.27 (minimum version 1.12)
 Go version:   go1.7.5
 Git commit:   c6d412e
 Built:        Fri Mar 24 00:00:50 2017
 OS/Arch:      linux/amd64
 Experimental: true
 ```

or set the DOCKER_HOST environment variable 

```
$ export DOCKER_HOST=tcp://localhost
$ docker version
Client:
 Version:      17.03.1-ce
 API version:  1.27
 Go version:   go1.7.5
 Git commit:   c6d412e
 Built:        Mon Mar 27 17:10:36 2017
 OS/Arch:      linux/amd64

Server:
 Version:      17.03.1-ce
 API version:  1.27 (minimum version 1.12)
 Go version:   go1.7.5
 Git commit:   c6d412e
 Built:        Fri Mar 24 00:00:50 2017
 OS/Arch:      linux/amd64
 Experimental: true
 ```

