# Base Image Python 3.9 Slim
FROM python:3.9-slim

# Install System Libraries for OpenCV (Debian Bookworm/Trixie Compatible)
RUN apt-get update && apt-get install -y \
    libgl1 \
    libglib2.0-0 \
    && rm -rf /var/lib/apt/lists/*

# Setup Non-Root User (Standard HF Security)
RUN useradd -m -u 1000 user
USER user
ENV PATH="/home/user/.local/bin:$PATH"

# Setup Working Directory
WORKDIR /app

# Install Dependencies
COPY --chown=user ./requirements.txt requirements.txt
RUN pip install --no-cache-dir --upgrade -r requirements.txt

# Copy Application Files
COPY --chown=user . /app

# Expose Port & Run
EXPOSE 7860
CMD ["python", "app.py"]