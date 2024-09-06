# First stage: build stage
FROM python:3.10-bullseye@sha256:bbc02da4025cdf20e97441210db50373d35b52b0b5e4f28e1eb0548b397f2679 AS build

# Set the working directory
WORKDIR /app

# Copy the requirements file
COPY requirements.txt .

# Install system dependencies
RUN apt-get update && apt-get install -y libpq-dev gcc
RUN pip install --no-cache-dir -r requirements.txt

# Second stage: runtime stage
FROM python:3.10-slim-bullseye@sha256:8e53874607bf1b7e97ad9fab4ee1bc3b237731e45b481e037dd2a30f603b0ac7

# Install system dependencies
RUN apt-get update && apt-get install -y libpq-dev

# Set the working directory
WORKDIR /app

# Copy the dependencies from the build stage
COPY --from=build /usr/local/lib/python3.10/site-packages /usr/local/lib/python3.10/site-packages
COPY --from=build /usr/local/bin /usr/local/bin

# Copy the application code
COPY app.py .

# Expose the application port
EXPOSE 5000

# Define the command to run the application
CMD ["python", "app.py"]