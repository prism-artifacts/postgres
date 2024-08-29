# Start with the Bitnami PostgreSQL image
FROM bitnami/postgresql:16.3.0-debian-12-r19

# Install dependencies to compile the aws_s3 extension
USER root
RUN apt-get update && apt-get install -y \
    postgresql-server-dev-all \
    build-essential \
    wget

# Download and install the aws_s3 extension
RUN wget https://s3.amazonaws.com/mountpoint-s3-release/latest/x86_64/mount-s3.deb && \
    apt-get install -y ./mount-s3.deb

# Clean up unnecessary packages
RUN apt-get remove -y build-essential wget \
    && apt-get autoremove -y 

# Switch back to the non-root user provided by the Bitnami image
USER 1001

# Expose PostgreSQL port
EXPOSE 5432
