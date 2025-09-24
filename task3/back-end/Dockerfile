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

# Install Flask-CORS to handle CORS issues
RUN pip3 install flask-cors

# Set working directory
WORKDIR /app

# Copy the Python API file
COPY ./app/api.py ./api.py

# Run the Flask application
CMD python3 api.py

# To build the Docker image, use the following command:
# sudo docker build -f ./back-end/Dockerfile -t softy-pinko-back-end:task3 ./back-end
# To run the Docker container, use the following command:
# sudo docker run -p 5252:5252 -it --rm --name softy-pinko-back-end-task3 softy-pinko-back-end:task3
