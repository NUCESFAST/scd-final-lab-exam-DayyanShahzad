# Dockerfile for Backend

# Use an official Node.js runtime as the base image
FROM node:14-alpine

# Set the working directory inside the container
WORKDIR /2393_backend

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install backend dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose the backend API on port 4393
EXPOSE 4593

# Start the backend server
CMD ["node", "index.js"]
