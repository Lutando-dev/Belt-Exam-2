# Use Nginx as the base image
FROM nginx:alpine

# Set the working directory inside the container
WORKDIR /usr/share/nginx/html

# Copy the static files into the container
COPY ./ui/* /usr/share/nginx/html

# Expose port 80 (the default port for Nginx)
EXPOSE 81

# This is the default command that will be executed when the container starts
CMD ["nginx", "-g", "daemon off;"]
