# Use an official base image with Python
FROM python:3.10-slim

# Set environment variables
ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8

# Install system dependencies
RUN apt-get update && \
    apt-get install -y \
    wget \
    build-essential \
    libz-dev \
    perl \
    git \
    && rm -rf /var/lib/apt/lists/*

# Install Kraken2
WORKDIR /opt
RUN wget https://github.com/DerrickWood/kraken2/archive/refs/tags/v2.1.2.tar.gz && \
    tar -xvzf v2.1.2.tar.gz && \
    cd kraken2-2.1.2 && \
    ./install_kraken2.sh /usr/local/bin

# Install Python dependencies
RUN pip install --no-cache-dir \
    matplotlib \
    pandas \
    biopython

# Set the working directory to /workspace (CodeAnywhere default)
WORKDIR /workspace

# Add Kraken2 to PATH
ENV PATH="/usr/local/bin/kraken2:$PATH"

# Default command
CMD ["bash"]
