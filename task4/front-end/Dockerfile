# Dockerfile for Nginx to serve the front-end application
FROM nginx:latest

# Copy the front-end files to the Nginx HTML directory
COPY ./softy-pinko-front-end /var/www/html/softy-pinko-front-end

# Copy the custom Nginx configuration file
COPY ./softy-pinko-front-end.conf /etc/nginx/conf.d/default.conf
