# Dockerfile for Nginx to serve the front-end application
FROM nginx:latest

# Copy the front-end files to the Nginx HTML directory
COPY ./softy-pinko-front-end /var/www/html/softy-pinko-front-end

# Copy the custom Nginx configuration file
COPY ./softy-pinko-front-end.conf /etc/nginx/conf.d/default.conf

# To build the Docker image, use the following command:
# sudo docker build -f ./front-end/Dockerfile -t softy-pinko-front-end:task2 ./front-end
# To run the Docker container, use the following command:
# sudo docker run -p 9000:9000 -it --rm --name softy-pinko-frontend softy-pinko-front-end:task2