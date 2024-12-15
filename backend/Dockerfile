# Stage 1: Build the app
FROM node:14 AS build

# Set working directory
WORKDIR /usr/src/app

# Install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the application code
COPY . .

# Stage 2: Create the final image
FROM alpine:3.16.7

# Install nodejs and npm in the final image
RUN apk add --no-cache nodejs npm

# Set working directory
WORKDIR /backend

# Copy the app from the build stage
COPY --from=build /usr/src/app /backend

# Prune npm dependencies and clean the cache
RUN npm prune --production && \
    npm cache clean --force && \
    rm -rf /tmp/*

# Expose the necessary port
EXPOSE 5000

# Start the application
CMD ["npm", "start"]

