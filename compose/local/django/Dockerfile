# Dockerfile
FROM python:3.10-alpine

ENV PYTHONUNBUFFERED=1

# Update apk and add system dependencies, including bash
RUN apk update && apk add --no-cache \
    gcc python3-dev musl-dev postgresql-dev \
    jpeg-dev zlib-dev freetype-dev lcms2-dev openjpeg-dev tiff-dev tk-dev tcl-dev \
    libffi-dev py-cffi \
    gettext \
    postgresql-client \
    build-base linux-headers \
    bash

# Upgrade pip and setuptools
RUN pip install --upgrade pip setuptools wheel

# Copy the requirements files into the container
COPY ./requirements /requirements

# Install Python dependencies
RUN pip install --no-cache-dir -r /requirements/local.txt

# Copy entrypoint and start scripts into the container
COPY ./compose/local/django/entrypoint /entrypoint
COPY ./compose/local/django/start /start

# Make the scripts executable
RUN chmod +x /entrypoint /start

# Set the working directory
WORKDIR /app

# Set the entrypoint
ENTRYPOINT ["/entrypoint"]
