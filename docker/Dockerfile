FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get install -y \
    unzip \
    graphviz \
    curl \
    musescore3 \
    python3-pip \
    python3-dev \
    build-essential \
    libhdf5-dev \
    pkg-config

RUN pip install --upgrade pip setuptools wheel

WORKDIR /app

COPY ./requirements.txt /app
RUN pip install --no-cache-dir --default-timeout=300 -r /app/requirements.txt

# Hack to get around tensorflow-io issue - https://github.com/tensorflow/io/issues/1755
RUN pip install tensorflow-io
RUN pip uninstall -y tensorflow-io

COPY /notebooks/. /app/notebooks
COPY /scripts/. /app/scripts

ENV PYTHONPATH="${PYTHONPATH}:/app"