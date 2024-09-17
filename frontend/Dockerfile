# First stage: build stage
FROM node:14@sha256:a158d3b9b4e3fa813fa6c8c590b8f0a860e015ad4e59bbce5744d2f6fd8461aa AS build

# Set the working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package.json .
RUN npm install

# Copy the application code
COPY . .

# Build the application
RUN npm run build

# Second stage: runtime stage
FROM node:14-slim@sha256:198142146b4c47193348f6415da769bdb5035c16fcab051c38c256a6b48f2e1c

# Set the working directory
WORKDIR /app

# Copy the built application from the build stage
COPY --from=build /app/dist /app/dist
COPY --from=build /app/node_modules /app/node_modules

# Expose the application port
EXPOSE 3000

# Define the command to run the application
CMD ["node", "dist/index.js"]