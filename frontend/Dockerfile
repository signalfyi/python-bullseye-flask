# First stage: build stage
FROM node:14 AS build

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
FROM node:14-slim

# Set the working directory
WORKDIR /app

# Copy the built application from the build stage
COPY --from=build /app/dist /app/dist
COPY --from=build /app/node_modules /app/node_modules

# Expose the application port
EXPOSE 3000

# Define the command to run the application
CMD ["node", "dist/index.js"]