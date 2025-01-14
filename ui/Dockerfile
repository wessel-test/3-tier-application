# Use Node.js as the base image
FROM node:14 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json first for caching purposes
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of your frontend files
COPY . .

# Build the application (assuming you have a build script defined in package.json)
RUN npm run build

# Use Nginx to serve the built application
FROM nginx:alpine

# Copy built files from the previous stage to Nginx's html directory
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80 to serve the application
EXPOSE 80

# Start Nginx when the container runs
CMD ["nginx", "-g", "daemon off;"]
