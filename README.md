# minio-examples

Some sample configurations of minio on docker demonstrating various features.

## /console

This folder has a docker compose that demonstrates how to setup minio console, with prometheus.

## /swarm

This has an example of how to deploy minio using docker 20.10 features to deploy a single docker service with 4 replicas, that can either be configured to run on a single node swarm, using uniquely named volumes, or on a multi node swarm, where each node that must run minio is expected to have a label.

## /tls

This example sets up minio using openssl to create a self signed cert, and minio serves https.
