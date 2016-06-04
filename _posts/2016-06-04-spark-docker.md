---
layout: post
title: Quick-start Apache Spark Environment Using Docker Containers
---

Are you learning or experimenting with [Apache Spark](http://spark.apache.org/)? Do you want to quickly use Spark with a [Jupyter iPython Notebook](http://jupyter.org/) and [Pyspark](https://spark.apache.org/docs/0.9.0/python-programming-guide.html), but don't want to go through a lot of complicated steps to install and configure your computer? Are you in the same position as many of my Metis classmates: you have a Linux computer and are struggling to install Spark? One option that allows you to get started quickly with writing Python code for Apache Spark is using Docker containers. Additionally, using this approach will work almost the same on Mac, Windows, and Linux.

Curious how? Let me show you!

# Install Docker

First you'll need to install Docker. Browse to the [Docker website](https://www.docker.com/) and click the green "Get Started" button in the top right. At the very least, you'll want to complete the "Install Docker" section, but I recommend going through the entire "Get Started" guide if you have the time as it will allow you to better understand the Docker commands we'll be using.

<amp-img width="650" height="327" layout="responsive" src="/assets/images/docker-spark/docker_get_started.png"></amp-img>

You can validate you installed Docker successfully by running a Docker container with the `hello-world` Docker image as follows.

~~~
$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
535020c3e8ad: Pull complete
af340544ed62: Pull complete
Digest: sha256:a68868bfe696c00866942e8f5ca39e3e31b79c1e50feaee4ce5e28df2f051d5c
Status: Downloaded newer image for hello-world:latest

Hello from Docker.
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
1. The Docker Engine CLI client contacted the Docker Engine daemon.
2. The Docker Engine daemon pulled the "hello-world" image from the Docker Hub.
3. The Docker Engine daemon created a new container from that image which runs the
   executable that produces the output you are currently reading.
4. The Docker Engine daemon streamed that output to the Docker Engine CLI client, which sent it
   to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
$ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker Hub account:
https://hub.docker.com

For more examples and ideas, visit:
https://docs.docker.com/userguide/
~~~

# Run the Docker container

We'll use the [jupyter/pyspark-notebook][1] Docker image. The great thing about this image is it includes:
- Apache Spark
- Jupyter Notebook
- Miniconda with Python 2.7.x and 3.x environments
- Pre-installed versions of pyspark, pandas, matplotlib, scipy, seaborn, and scikit-learn
- [Additional goodies][1]

Create a new folder somewhere on your computer. You'll store the Jupyter notebooks you create and other Python code to interact with Spark in this folder. I created my folder in my home directory as shown below, but you should be able to create the folder almost anywhere (although I would avoid any directories that require elevated permissions).

    $ cd ~
    $ pwd
    /Users/maxmelnick

    $ mkdir spark-docker && cd $_

    $ pwd
    /Users/maxmelnick/spark-docker

To run the container, all you need to do is execute the following:

    $ docker run -d -p 8888:8888 -v $PWD:/home/jovyan/work --name spark jupyter/pyspark-notebook

What's going on when we run that command?

The `-d` runs the container in the background.

The `-p 8888:8888` makes the container's port `8888` accessible to the host (i.e., your local computer) on port `8888`. This will allow us to connect to the Jupyter Notebook server since it listens on port `8888`.

The `-v $PWD:/home/jovyan/work` allows us to map our `spark-docker` folder (which should be our current directory - $PWD) to the container's `/home/joyvan/work` working directory (i.e., the directory the Jupyter notebook will run from). This makes it so notebooks we create are accessible in our `spark-docker` folder on our local computer. It also allows us to make additional files such as data sources (e.g., CSV, Excel) accessible to our Jupyter notebooks.

The `--name spark` gives the container the name `spark`, which allows us to refer to the container by name instead of ID in the future.

The final part of the command, `jupyter/pyspark-notebook` tells Docker we want to run the container from the `jupyter/pyspark-notebook` image.

For more information about the `docker run` command, check out the [Docker docs](https://docs.docker.com/engine/reference/commandline/run/).

# Test Spark in a Jupyter notebook using Pyspark

The [jupyter/pyspark-notebook][1] image automatically starts a Jupyter Notebook server. In order to get the URL of the server, we need to figure out what IP address the Docker container is running on. Getting the IP is slightly different depending on what O/S you're running.

### Mac or Windows

> **Note:** As of this writing (June 4, 2016), the following command is the proper way to get the Docker Machine IP address on Mac or Windows. However, Docker is slated to release a [native Docker version for Mac or Windows](https://blog.docker.com/2016/03/docker-for-mac-windows-beta/) in the near future. In the native version, the `docker-machine` command will not work and you will most likely have to use the `docker inspect` command per the Linux section below.

    $ docker-machine ip
    192.168.99.100 # This was mine, but won't necessarily be the same IP for you

> Alternatively from the command above, you may be able to streamline the process with the following command that automatically gets the proper IP and opens a new browser window to the correct address all in one step.
>
>   `$ open "http://$(docker-machine ip):8888"`

### Linux


    $ docker inspect --format '{% raw %}{{ .NetworkSettings.IPAddress }}{% endraw %}' spark
    172.17.0.2 # This is an example output, but won't necessarily be the same IP for you


## Open Jupyter in your browser

Next, open a browser to `http://[YOUR_DOCKER_MACHINE_IP_ADDRESS]:8888`, filling in [YOUR_IP_ADDRESS] as appropriate. You should see the Jupyter home page.

## Test using Spark in Jupyter

Once you have the Jupyter home page open, create a new Jupyter notebook using either `Python 2` or `Python 3`.

<amp-img width="650" height="264" layout="responsive" src="/assets/images/docker-spark/new_jupyter_notebook.png"></amp-img>

In the first cell, run the following code. The result should be five integers randomly sampled from 0-999, but not necessarily the same as what's below.

~~~python
import pyspark
sc = pyspark.SparkContext('local[*]')

# do something to prove it works
rdd = sc.parallelize(range(1000))
rdd.takeSample(False, 5)
~~~




    [841, 378, 942, 629, 399] # Output

That's it! Now you can start learning and experimenting with Spark!

# An alternative approach on Mac

Using the Docker [jupyter/pyspark-notebook][1] image enables a cross-platform (Mac, Windows, and Linux) way to quickly get started with Spark code in Python. If you have a Mac and don't want to bother with Docker, another option to quickly get started with Spark is using Homebrew and Find spark. Check out the [Find spark documentation](https://github.com/minrk/findspark) for more details.


# Conclusion

As you can see, Docker allows you to quickly get started using Apache Spark in a Jupyter iPython Notebook, regardless of what O/S you're running. My hope is that you can use this approach to spend less time trying to install and configure Spark, and more time learning and experimenting with it. Best of luck!

[1]: https://github.com/jupyter/docker-stacks/tree/master/pyspark-notebook