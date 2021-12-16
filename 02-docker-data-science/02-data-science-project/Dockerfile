# Use latest miniconda image as parent
# miniconda is python + conda installer
FROM continuumio/miniconda3

# Upgrading pip as 3.6 has the version 10.0.1
RUN pip install --upgrade pip

# Meta-data
LABEL maintainer="Rehan Fazal <rehanfazal@live.com>" \
      description="Docker Data Science Workflow"

# Set the working directory to /app
WORKDIR /app

# Install the required libraries
RUN conda install jupyter -y && \
    conda install pandas -y && \
    conda clean -y -all

# Make port 8888 available to the world outside this container
EXPOSE 8888

# Create mountpoint
VOLUME /app

# Run jupyter when container launches
CMD ["jupyter", "notebook", "--ip='*'", "--port=8888", "--no-browser", "--allow-root"]
