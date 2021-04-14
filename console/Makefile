salt = $(shell cat /dev/urandom | base64 | tr -dc A-Za-z0-9 | head -c 16)
files = .env.local
minio_root_user = admin
minio_root_password = admin123
minio_console_user = console
minio_console_password = console123

up: $(files)
	MINIO_ROOT_USER=$(minio_root_user) \
	MINIO_ROOT_PASSWORD=$(minio_root_password) \
	docker-compose up -d minio prometheus console
	sleep 20
	open http://localhost:8080
	open http://localhost:9000
	open http://localhost:9090

.env.local:
	echo CONSOLE_PBKDF_PASSPHRASE=$(salt) > .env.local
	echo CONSOLE_PBKDF_SALT=$(salt) >> .env.local

init:
	docker-compose run mc alias set myminio http://minio:9000 $(minio_root_user) $(minio_root_password)
	docker-compose run mc admin policy add myminio consoleAdmin policy/admin.json
	docker-compose run mc admin user add myminio $(minio_console_user) $(minio_console_password)
	docker-compose run mc admin policy set myminio consoleAdmin user=$(minio_console_user)

clean:
	docker-compose down -v
	rm $(files)
