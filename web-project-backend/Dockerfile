# Use an official Node.js 18 image as the base
FROM node:18-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json first
# This uses Docker's layer caching to speed up builds
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of your application code
COPY . .

# Your app runs on port 8080 according to your .env file
EXPOSE 8080

# The command to start your app (from your package.json)
CMD [ "node", "./bin/www" ]