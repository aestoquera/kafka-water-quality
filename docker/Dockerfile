# Base image
FROM ubuntu:22.04

# Set environment variables
ENV DEBIAN_FRONTEND=noninteractive
ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64

# Install dependencies
RUN apt-get update && apt-get install -y \
    openjdk-11-jdk \
    wget \
    python3-pip \
    curl && \
    apt-get clean

# Install Kafka
WORKDIR /opt
RUN wget https://archive.apache.org/dist/kafka/3.4.0/kafka_2.12-3.4.0.tgz && \
    tar -xvf kafka_2.12-3.4.0.tgz && \
    mv kafka_2.12-3.4.0 kafka && \
    rm kafka_2.12-3.4.0.tgz

#Add assignment files
COPY assignment_files/water_data_producer_pr2.ipynb ./water_data_producer_pr2.ipynb
COPY assignment_files/water_data_consumer_pr2.ipynb ./water_data_consumer_pr2.ipynb
COPY assignment_files/aeration_classifier.joblib ./aeration_classifier.joblib

# Set environment variables for Kafka
ENV KAFKA_HOME=/opt/kafka
ENV PATH=$PATH:$KAFKA_HOME/bin

# Uprade pip and install dependencies
RUN pip3 install --upgrade pip
COPY requirements.txt /requirements.txt
RUN pip3 install -r /requirements.txt

# Expose ports
EXPOSE 2181 9092 8888

RUN ls

# Add entrypoint script
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
RUN sed -i 's/\r$//' /entrypoint.sh

# Default command
CMD ["/entrypoint.sh"]
