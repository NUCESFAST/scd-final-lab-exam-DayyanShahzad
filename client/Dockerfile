# Dockerfile for Frontend

# Use an official Node.js runtime as the base image
FROM node:14-alpine

# Set the working directory inside the container
WORKDIR /2393_frontend

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install frontend dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the frontend assets
RUN npm run build

# Expose the application on port 2393
EXPOSE 2393

# Start the application
CMD ["npm", "start"]
