# Stage 1: Build the Angular application
FROM node:18 AS builder

# Set working directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy application code
COPY . .

# Build the application
RUN npm run build

# Stage 2: Serve the application using Nginx
FROM nginx:alpine

# Copy the built Angular application to Nginx's HTML directory
COPY --from=builder /app/dist/angular-15-crud /usr/share/nginx/html

# Use default Nginx configuration for serving static files
# Remove custom Nginx configuration since we're using a separate reverse proxy

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]