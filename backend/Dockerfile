# Use a stable and efficient Python base image
FROM python:3.12-slim-bookworm

# Disable .pyc files and enable stdout logs
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Set working directory inside the container
WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y curl && apt-get clean

# Optional: use uv for fast dependency installation (recommended)
COPY --from=ghcr.io/astral-sh/uv:latest /uv /bin/uv

# Copy only requirements first for caching
COPY requirements.txt .

# Use uv to install dependencies quickly
RUN uv pip install -r requirements.txt --system

# Copy the rest of the project files
COPY . .

# Expose Django development server port
EXPOSE 8000

# Run Django server
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
