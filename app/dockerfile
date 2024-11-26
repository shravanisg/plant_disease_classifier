# Start with a base image that includes Python
FROM python:3.9-slim

# Set environment variables
ENV LANG=C.UTF-8
ENV PYTHONUNBUFFERED=1

# Install necessary dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    ca-certificates \
    netbase \
    tzdata \
    gcc \
    libbz2-dev \
    libc6-dev \
    libdb-dev \
    libffi-dev \
    libgdbm-dev \
    liblzma-dev \
    libncursesw5-dev \
    libreadline-dev \
    libsqlite3-dev \
    libssl-dev \
    make \
    tk-dev \
    uuid-dev \
    wget \
    xz-utils \
    zlib1g-dev && \
    rm -rf /var/lib/apt/lists/*

# Set the working directory in the container
WORKDIR /app

# Copy the dependencies file into the container
COPY /app/requirements.txt /app/requirements.txt

# Install Python dependencies
RUN pip install --no-cache-dir -r /app/requirements.txt

# Copy the project files into the container
COPY /app/api.py /app/api.py
COPY /app/plant_disease /app/plant_disease
COPY /app/class_indices.json /app/class_indices.json

# Expose the port your app will run on
EXPOSE 8000

# Command to run the app (e.g., using uvicorn for a FastAPI app)
CMD ["uvicorn", "api:app", "--host", "0.0.0.0", "--port", "8000"]
