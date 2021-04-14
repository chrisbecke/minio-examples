# Minio on Docker Swarm examples

## Quickstart

First, create credentials. These will be deployed to swarm as docker secrets.

```bash
cat minio_user > access_key.txt
cat minio_password > access_key.txt
```

### Deploy onto a singlenode

To deploy minio to a singlenode docker swarm.

```bash
docker stack deploy -c minio-stack.yml -c minio-stack-singlenode.yml minio-swarm-example
```

Then connect to [localhost:9000](http://localhost:9000) in the browser to access the minio gui.

This stack achieves per-instance persistence using `{{.Task.Slot}}` to number each data volume.

### Deploy onto multiple nodes

To deploy minio to multi node docker swarm, first apply a `minio=true` to the 4 nodes that have a data volume, or sufficient space.

```bash
docker node update --label-add "minio=true" node1
docker node update --label-add "minio=true" node2
docker node update --label-add "minio=true" node3
docker node update --label-add "minio=true" node4
```

Update `minio-stack-multinode.yml` with the location of your minio data mounts on each node:

```yml
volumes:
  data:
    driver: local
    driver_opts:
      type: none
      o: bind
      device: /mnt/minio-disk/
```

Deploy the stack to your swarm...

```bash
docker stack deploy -c minio-stack.yml -c minio-stack-multinode.yml minio-swarm-example
```

Then connect to [localhost:9000](http://localhost:9000) in the browser to access the minio gui.
