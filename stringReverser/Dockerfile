# Use Python 3.7.1 as the base image
FROM python:3.12.1

# Create a directory for the application
RUN mkdir /app

# Set the working directory to /app
WORKDIR /app

# Update package lists and install Python dependencies
RUN apt-get update -y && \
    apt-get install -y python3-pip python-dev-is-python3

# Copy the requirements.txt file to the container
# This step is separated to leverage Docker cache
COPY ./requirements.txt /app/requirements.txt

# Install Python dependencies from requirements.txt
RUN pip install -r requirements.txt

# Add the application code to the container
ADD . /app

# Expose port 5000 to allow external access
EXPOSE 5000

# Set the default command to run when the container starts
CMD flask run --host=0.0.0.0
