# Use the official PostgreSQL 16 image as the base
FROM postgres:16

# Install required packages
RUN apt-get update && apt-get install -y \
    python3 python3-dev python3-pip \
    postgresql-server-dev-16 \
    build-essential \
    git \
    python3-boto3 \
    postgresql-plpython3-16

# Clone the postgres-aws-s3 repository and install the extension
RUN git clone https://github.com/chimpler/postgres-aws-s3.git /usr/src/postgres-aws-s3
WORKDIR /usr/src/postgres-aws-s3
COPY aws_s3* .
COPY Makefile .
RUN make && \
    make install

# Create the plpython3u and aws_s3 extensions in the default database
RUN echo "CREATE EXTENSION plpython3u;" >> /docker-entrypoint-initdb.d/init-extensions.sql && \
    echo "CREATE EXTENSION aws_s3;" >> /docker-entrypoint-initdb.d/init-extensions.sql

# Expose PostgreSQL port
EXPOSE 5432

# Set the default command to run PostgreSQL
CMD ["postgres"]