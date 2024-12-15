# Build stage
FROM node:14 AS build

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json files to the container
COPY package*.json ./

# Install application dependencies
RUN npm install

# Copy the rest of the application code to the container
COPY . .

# Final production stage
FROM alpine:3.16.7

# Set the working directory for the production stage
WORKDIR /backend

# Install nodejs and npm in the production image
RUN apk update && apk add --update nodejs

# Copy the necessary files from the build stage
COPY --from=build /usr/src/app /backend

# Set the environment variable for the app
ENV NODE_ENV=production

# Expose the port used by the app
EXPOSE 5000

# Install production dependencies only, clear cache, and prune node_modules
RUN npm prune --production && \
    npm cache clean --force && \
    rm -rf /tmp/*

# Start the application
CMD ["npm", "start"]

