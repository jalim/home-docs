+++
title = 'Running Minio on QNAP'
date = 2024-01-14T09:07:07+01:00
+++
## Introduction

I wanted to backup my Kubernetes volumes to my old QNAP NAS but QNAP doesn’t really support easy ways to backup from my truenas NAS so I setup a docker container on QNAP that I can then address as s3 storage from volsync restic.

The below snippet is what I used to get it working:

```console
sudo docker run -d \

    —restart=always \

    -p 9000:9000 \

    -p 9001:9001 \

    —name minio-docker \

    -e MINIO_ROOT_USER=minio \

    -e MINIO_ROOT_PASSWORD=password \

    -v /share/minio:/data \

    minio/minio server /data \

    —console-address :9001

```