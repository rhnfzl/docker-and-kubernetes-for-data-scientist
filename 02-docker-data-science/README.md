# Docker Workflows for Data Science

Jupyter notebooks are ideal for sharing the findings of data analysis. However, in order for our notebooks to function, users must have access to data as well as all of the dependencies that were needed to generate the initial computations.

Docker is used to package our notebook, data, and dependencies into a single image. This image may be uploaded to [Docker Hub](https://hub.docker.com/).


## A: Self-Contained Container


### Create Docker Hub Account

1. Go to [https://hub.docker.com/](https://hub.docker.com/)

2. Sign up for an account


### Downloading Notebook and Data

1. In the new folder save a copy of the [notebook](/02-docker-data-science/iris/iris-analysis.ipynb) in the folder.

2. Create a subfolder called data and save a copy of [`iris.csv`](/02-docker-data-science/iris/data/iris.csv)

### Create Dockerfile

[`Dockerfile`](https://docs.docker.com/engine/reference/builder/) is a file that contains commands that are used to build a Docker image.

1. Create a `Dockerfile` in the new folder.

2. Specify the image on which it need to build off. In here use the `python:3.6.5-slim` image as a base.

3. Next set the working directory and copy in the contents of our current directory into the working directory.

```Dockerfile
WORKDIR /app
COPY . /app
```

4. Install dependencies via `pip`:

```Dockerfile
RUN pip --no-cache-dir install numpy pandas seaborn sklearn jupyter
```

***Tip:** Always clear cache when building an image*

5. In order to connect to the Jupyter instance that is running inside of the container, we will need to set up port forwarding

```Dockerfile
EXPOSE 8888
```

6. Setup to start Jupyter when the container launches:

```Dockerfile
CMD ["jupyter", "notebook", "--ip='*'", "--port=8888", "--no-browser", "--allow-root"]
```

7. Directory structure looks as follows:

```
.
├── Dockerfile
├── data
│   └── iris.csv
└── iris-analysis.ipynb
```

### Build Image

> Recall that `docker build` creates an image from a `Dockerfile`

1. From this new folder directory, build an image as follows:

`docker build -t [docker-hub-user-name]/[new folder] .`

2. Test image was built successfully by creating a container:

`docker run -p 8888:8888 [docker-hub-user-name]/[new folder]`

3. Confirm we can open the notebook and recalculate cells by going to the URL of the Jupyter process running in the container.

4. `Ctrl+c` to stop the process.


### Push Image to Docker Hub

1. Log in to your user account using `docker login`

2. Push image to Docker Hub using `docker push`

```
docker push [docker-hub-user-name]/[new folder]
```

Users will be able to download the image using `docker pull`.


## B: Data Science Project

Using Docker, we can create a project / team image with our development environment and mount a volume with our notebooks and data.

The benefits of this workflow are that we can:
* Separate out projects
* Spin up a container to onboard new employees
* Build an automated testing pipeline to confirm upgrade dependencies do not break code

### Create Dockerfile

1. Create a new folder for this project:

2. Create a `Dockerfile` in the new folder folder

3. We need to specify which image we are building off of.

```dockerfile
FROM python:3.6.5-slim
```

4. Set the working directory:

```dockerfile
WORKDIR /app
```

5. `pip install` some required libraries, make sure to clean up the cache.

```dockerfile
RUN pip --no-cache-dir install pandas jupyter
```

6. In order to connect to the Jupyter instance that is running inside of the container, we will need to set up port forwarding.

```dockerfile
EXPOSE 8888
```

7. Create a mountpoint inside of our container:

```dockerfile
VOLUME /app
```

8. Start Jupyter when the container launches:

```Dockerfile
CMD ["jupyter", "notebook", "--ip='*'", "--port=8888", "--no-browser", "--allow-root"]
```

9. Confirm directory structure looks as follows:

```
.
└── Dockerfile
```

### Build Image

1. In the new folder, build an image as follows:

`docker build -t [new folder] .`

2. Test image was built successfully by creating a container and mounting a directory. For this, you use the full path to a directory on your machine.

`docker run -p 8888:8888 -v /full/local/path:/app [new folder]`
docker run -p 8888:8888 -v /full/local/path:/app 02-data-science-project

3. Confirm the access to the Jupyter process by going to the endpoint URL in the container output. 

4. `Ctrl+c` to stop the process

# Data Science Essentials

1. Navigate to this folder on your local machine.

2. Build the Dockerfile and start the container.

```
docker build -t talk_recommender .
docker run -p 8888:8888 -p 9000:9000 -v [choose a password]:/app talk_recommender
```

3. Take the url from the log and load up the Jupyter notebook `talk_recommender.ipynb` in your browser.







