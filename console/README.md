# Console

This is meant to create a configured minio with console instance with docker compose.

Full docs here [MinIO Console](https://github.com/minio/console).

## Quickstart

With make

```bash
cd console
make init up
```

Then, open [minio](http://localhost:9000), [console](http://localhost:8080), and [prometheus](http://localhost) in a browser to verify everything is working.
The minio credentials if not changed are `admin`, `Password1234` and the console user is `console`, `console123`.
