# Stage 1: Build stage
FROM node:11.10.0-alpine AS build-stage

# Install necessary dependencies
RUN apk add --update --no-cache \
    python \
    make \
    g++

# Copy application source code
COPY . /src

# Set working directory
WORKDIR /src

# Copy package.json and package-lock.json (or yarn.lock)
COPY ./package* ./

# Install Node.js dependencies
RUN npm install

# Build the application
RUN yarn build

# Stage 2: Production stage
FROM nginx:latest

# Remove default NGINX website
RUN rm -rf /usr/share/nginx/html

# Create directory for the application
RUN mkdir /usr/share/nginx/html

# Copy built files from the build stage to NGINX's default directory
COPY --from=build-stage /src/build/ /usr/share/nginx/html/

# Copy NGINX configuration file
COPY default.conf /etc/nginx/conf.d/

# Expose port 80 for web traffic
EXPOSE 80