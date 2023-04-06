COMPOSE_FILE:=multi-docker-compose.yml
COMPOSE_PROFILES:=nonode
ARGS?="-d"
UPDOWN?="up"


default:
	@echo "Makefile Help:\n\n";
	@grep '^# Target:' Makefile | sed -e 's/^# Target: //'

# Target: onenode - setup a single node cluster with console
onenode:
	@make -e COMPOSE_PROFILES=$@  $(UPDOWN) 

# Target: twonode - setup a two node cluster with console
twonode:
	@make -e COMPOSE_PROFILES=$@  $(UPDOWN)

# Target: threenode - setup a three node cluster with console
threenode:
	@make -e COMPOSE_PROFILES=$@  $(UPDOWN) 

# Target: fournode - setup a four node cluster with console
fournode:
	@make -e COMPOSE_PROFILES=$@  $(UPDOWN) 

# Target: fivenode - setup a five node cluster with console
fivenode:
	@make -e COMPOSE_PROFILES=$@  $(UPDOWN) 

# Target: status - show running instances
status:
	@docker ps

up: 
	COMPOSE_FILE=$(COMPOSE_FILE) SEEDS=redpanda-0:33145 LOG_LEVEL=warn COMPOSE_PROFILES=$(COMPOSE_PROFILES) docker compose up $(ARGS)

down:
	COMPOSE_FILE=$(COMPOSE_FILE) SEEDS=redpanda-0:33145 LOG_LEVEL=warn COMPOSE_PROFILES=$(COMPOSE_PROFILES) docker compose down

# Target: clean - shutdown nodes and clean up/purge volumes -- WARNING: this is destructive
clean: COMPOSE_PROFILES=fivenode
clean:
	make -e COMPOSE_PROFILES=fivenode down
	docker ps -a --filter name=redpanda --format "{{.Names}}" | xargs docker rm -v
	COMPOSE_FILE=$(COMPOSE_FILE) SEEDS=redpanda-0:33145 LOG_LEVEL=warn COMPOSE_PROFILES=$(COMPOSE_PROFILES) docker volume prune -f
