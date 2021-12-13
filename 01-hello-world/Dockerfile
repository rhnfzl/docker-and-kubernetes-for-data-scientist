# EACH COMMAND CREATES A NEW IMAGE LAYER

# Use latest Python runtime as base image
FROM python:3.6.5-alpine3.7

# Set the working directory to /app
WORKDIR /app

# Copy current dir
COPY . /app

# Run hello_world.py when the container launches
CMD ["python", "hello_world.py"]
