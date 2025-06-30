# Use Python 3.12 slim as base image
FROM python:3.12-slim

# Update package index and install required system packages including libpcap for Scapy
RUN apt-get update && apt-get install -y git procps socat iproute2 netcat-openbsd libpcap-dev

# Set working directory for cloning repositories
WORKDIR /app/repos

# Clone both projects into the same parent folder
RUN git clone --single-branch https://github.com/thomas-hoger/CTD-5G.git 
RUN git clone --single-branch https://github.com/jdegre/5GC_APIs.git

WORKDIR /app/repos/CTD-5G

# Install Python dependencies for CTD-5G
RUN pip install --no-cache-dir -r requirements.txt

# Default command — adjust this to what your container should actually run
CMD ["sh", "-c", "while true; do nc -l -p 8080; done"]
