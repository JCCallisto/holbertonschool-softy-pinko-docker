# Use the latest Ubuntu as base image
FROM ubuntu:latest

# Update package list
RUN apt-get update

# Upgrade installed packages
RUN apt-get upgrade -y

# Install Python3 and pip3
RUN apt-get install -y python3 python3-pip

# Remove the externally managed environment restriction
RUN rm /usr/lib/python*/EXTERNALLY-MANAGED

# Install Flask using pip3
RUN pip3 install flask

# Set working directory
WORKDIR /app

# Copy the Python API file
COPY ./api.py /app/api.py

# Run the Flask application
CMD python3 api.py
