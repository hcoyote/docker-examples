COMPOSE_FILE:=multi-docker-compose.yml
COMPOSE_PROFILES:=nonode

#onenode: COMPOSE_PROFILES:=onenode

onenode:
	@make -e COMPOSE_PROFILES=$@  up

twonode:
	@make -e COMPOSE_PROFILES=$@  up

threenode:
	@make -e COMPOSE_PROFILES=$@  up

fournode:
	@make -e COMPOSE_PROFILES=$@  up

fivenode:
	@make -e COMPOSE_PROFILES=$@  up

up: 
	COMPOSE_FILE=$(COMPOSE_FILE) SEEDS=redpanda-0:33145 LOG_LEVEL=warn COMPOSE_PROFILES=$(COMPOSE_PROFILES) docker compose up

down:
	COMPOSE_FILE=$(COMPOSE_FILE) SEEDS=redpanda-0:33145 LOG_LEVEL=warn COMPOSE_PROFILES=$(COMPOSE_PROFILES) docker compose down

purge: COMPOSE_PROFILES=fivenode
purge:
	make -e COMPOSE_PROFILES=fivenode down
	docker ps -a --filter name=redpanda --format "{{.Names}}" | xargs docker rm -v
	COMPOSE_FILE=$(COMPOSE_FILE) SEEDS=redpanda-0:33145 LOG_LEVEL=warn COMPOSE_PROFILES=$(COMPOSE_PROFILES) docker volume prune -f
