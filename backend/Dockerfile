# First stage: build stage
FROM python:3.10-bullseye@sha256:e31fc403976a31a44cb63e8c7b30d7322b1244fe50f76bb14ce17eebc4d3ea94 AS build

# Set the working directory
WORKDIR /app

# Copy the requirements file
COPY requirements.txt .

# Install system dependencies
RUN apt-get update && apt-get install -y libpq-dev gcc
RUN pip install --no-cache-dir -r requirements.txt

# Second stage: runtime stage
FROM python:3.10-slim-bullseye@sha256:aefd4c44c655edfa34854a36bc3b50391e96e3cff9d967e836f4c7c5b9c3c122

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