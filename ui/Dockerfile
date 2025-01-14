# Use Nginx as the base image
FROM nginx:alpine

# Remove the default Nginx configuration
RUN rm /etc/nginx/conf.d/default.conf

# Copy your static files from the current directory to Nginx's HTML directory
COPY . /usr/share/nginx/html

# Expose port 80 to serve the application
EXPOSE 80

# Start Nginx when the container runs
CMD ["nginx", "-g", "daemon off;"]

