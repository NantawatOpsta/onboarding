FROM python:3.14-slim

# Create a non-root user id 1000
RUN useradd -m -u 1000 app

# Create the app directory
RUN mkdir /app

# Change ownership of the app directory to the non-root user
RUN chown -R app:app /app

# Set the working directory
WORKDIR /app

# Set environment variables to optimize Python
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1 

# Upgrade pip and install dependencies
RUN pip install --upgrade pip

# Copy the requirements file first (better caching)
COPY requirements.txt /app/

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt