# Console

This is meant to create a configured minio with console instance with docker compose.

Full docs here [MinIO Console](https://github.com/minio/console).

## Quickstart With make

```bash
cd console
make init up
```

Then, open [minio](http://localhost:9000), [console](http://localhost:8080), and [prometheus](http://localhost) in a browser to verify everything is working.
The minio credentials if not changed are `admin`, `admin123` and the console user is `console`, `console123`.

## Without Make

Create a .env.local file if it does not exist, with the following contents

```
CONSOLE_PBKDF_PASSPHRASE=some-secret
CONSOLE_PBKDF_SALT=some-secret
```

Start minio

```bash
docker-compose up -d minio console prometheus
```

Use the `mc` embedded in the docker-compose to create the  console user.

```bash
docker-compose run mc alias set myminio http://minio:9000 admin admin123
docker-compose run mc admin policy add myminio consoleAdmin policy/admin.json
docker-compose run mc admin user add myminio console console123
docker-compose run mc admin policy set myminio consoleAdmin user=console
```

Now, open [console](http://localhost:8080) with the credentials `console`, `console123` to verify console has loaded and the stats are displaying.

If they are not, check [prometheus](http://localhost) - the Status > Targets menu should show minio:9000 as up.
And/or [minio](http://localhost:9000) with the credentials `admin`, `admin123`.

## Alternate scrape paths

* /minio/v2/metrics/cluster
* /minio/v2/metrics/node
* /minio/prometheus/metrics

Edit `prometheus/prometheus.yml` with the alternate scrape path, and then restart prometheus to pick up the new config

```bash
docker-compose kill -s SIGHUP prometheus
```
