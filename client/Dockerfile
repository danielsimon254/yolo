# Build stage
FROM node:16-alpine3.16 as build-stage

# Set the working directory inside the container
WORKDIR /client

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies and clears the npm cache and removes any temporary files
RUN npm install && \
    npm cache clean --force && \
    rm -rf /tmp/*

# Copy the rest of the application code
COPY . .

# Build the application and remove development dependencies
RUN npm run build && \
    npm prune --production

# Final production stage
FROM alpine:3.16.7 as production-stage

# Install npm in the production image
RUN apk update && apk add npm

WORKDIR /client

# Copy only the necessary files from the build stage
COPY --from=build-stage /client/build ./build
COPY --from=build-stage /client/public ./public
COPY --from=build-stage /client/src ./src
COPY --from=build-stage /client/package*.json ./

# Set the environment variable for the app
ENV NODE_ENV=production

# Expose the port used by the app
EXPOSE 3000
ENV HOST=localhost
# Start the application
CMD ["npm", "start"]

