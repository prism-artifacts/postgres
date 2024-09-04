# Start with the Bitnami PostgreSQL image
FROM public.ecr.aws/docker/library/postgres:latest

# Install dependencies to compile the aws_s3 extension
RUN apt-get update && \ 
    apt-get install -y awscli wget

# Download and install the aws_s3 extension
RUN wget https://s3.amazonaws.com/mountpoint-s3-release/latest/x86_64/mount-s3.deb && \
    apt-get install -y ./mount-s3.deb

# Expose PostgreSQL port
EXPOSE 5432

# Set the default command to run PostgreSQL
CMD ["postgres"]