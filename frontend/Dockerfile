# First stage: build stage
FROM node:14@sha256:2cafa3fbb0b6529ee4726b4f599ec27ee557ea3dea7019182323b3779959927f AS build

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
FROM node:14-slim@sha256:21b6dc452bd2c066724bd5be0f7256ef81a068c47de1adead10a2f810557de02

# Set the working directory
WORKDIR /app

# Copy the built application from the build stage
COPY --from=build /app/dist /app/dist
COPY --from=build /app/node_modules /app/node_modules

# Expose the application port
EXPOSE 3000

# Define the command to run the application
CMD ["node", "dist/index.js"]