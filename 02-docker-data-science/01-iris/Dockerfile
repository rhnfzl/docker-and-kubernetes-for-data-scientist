# Use latest Python runtime as a parent image
FROM python:3.6.5-slim

# Upgrading pip as 3.6 has the version 10.0.1
RUN pip install --upgrade pip

# Meta-data
LABEL maintainer="Rehan Fazal <rehanfazal@live.com>" \
      description="Data Science Workflow #1: iris\
      Libraries, data, and code in one image"

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install the required libraries
RUN pip --no-cache-dir install numpy pandas seaborn sklearn jupyter

# Make port 8888 available to the world outside this container
EXPOSE 8888

# Run jupyter when container launches
CMD ["jupyter", "notebook", "--ip='*'", "--port=8888", "--no-browser", "--allow-root"]