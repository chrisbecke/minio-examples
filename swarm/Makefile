stack = minio-swarm-example
minio_root_user = root
minio_root_password = root1234

files = access_key.txt
files += secret_key.txt

mode = single

stack_files = minio-stack.yml

ifeq ($(mode),single)
stack_files += minio-stack-singlenode.yml
else
stackfiles += minio-stack-multinode.yml
endif

deploy: $(files)
	docker stack deploy $(addprefix --compose-file ,$(stack_files)) $(stack)

access_key.txt:
	echo "$(minio_root_user)" > access_key.txt

secret_key.txt:
	echo "$(minio_root_password)" > secret_key.txt

clean:
	docker stack rm $(stack)
	rm $(files)
