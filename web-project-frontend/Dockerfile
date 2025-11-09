# ----- Build Stage -----
FROM node:18-alpine AS build

WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the source code
COPY . .

# Build the app (from your package.json)
RUN npm run build

# ----- Serve Stage -----
FROM nginx:alpine

# Copy the built files from the 'build' stage
# Your vite build output is in the 'dist' folder
COPY --from=build /app/dist /usr/share/nginx/html

# We will add a custom Nginx config to handle React Router and proxy API calls
# Remove the default config first
RUN rm /etc/nginx/conf.d/default.conf

# Copy our new config file
COPY nginx.conf /etc/nginx/conf.d

# Expose port 80 (default Nginx port)
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]