.PHONY: clean
clean:
	docker-compose down
	rm -Rf ./postgres/data

.PHONY: build
build:
	cp -R ./../../api ./go-api/
	docker-compose build
	rm -Rf ./go-api/api
	# TODO add DDL

.PHONY: up
up:
	docker-compose up --remove-orphans -d

.PHONY: down
down:
	docker-compose down


.PHONY: exec
exec go:
	docker exec -it go-todo-api bash


.PHONY: logs
logs:
	docker-compose logs -f

.PHONY: start
start:
	make clean
	make build
	make up

