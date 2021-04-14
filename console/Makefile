salt = $(shell cat /dev/urandom | base64 | tr -dc A-Za-z0-9 | head -c 16)
files = .env.local

up: $(files)
	docker-compose up -d minio prometheus console
	sleep 20
	open http://localhost:8080
	open http://localhost:9000
	open http://localhost:9090

.env.local:
	echo CONSOLE_PBKDF_PASSPHRASE=$(salt) > .env.local
	echo CONSOLE_PBKDF_SALT=$(salt) >> .env.local

init:
	docker-compose run mc alias set myminio http://minio:9000 admin Password1234
	docker-compose run mc admin policy add myminio consoleAdmin policy/admin.json
	docker-compose run mc admin user add myminio console console123
	docker-compose run mc admin policy set myminio consoleAdmin user=console

clean:
	docker-compose down -v
	rm $(files)
