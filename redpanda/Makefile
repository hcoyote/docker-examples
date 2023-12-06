COMPOSE_FILE:=multi-docker-compose.yml
COMPOSE_PROFILES:=nonode
ARGS?="-d"
UPDOWN?=up
RP_VERSION?="v23.2.17"


default:
	@echo "Makefile Help:\n\n";
	@grep '^# Target:' Makefile | sed -e 's/^# Target: //'

# Target: onenode - setup a single node cluster with console
onenode:
	make -e COMPOSE_PROFILES=$@ -e RP_VERSION=$(RP_VERSION)  $(UPDOWN) 

# Target: twonode - setup a two node cluster with console
twonode:
	make -e COMPOSE_PROFILES=$@ -e RP_VERSION=$(RP_VERSION)  $(UPDOWN)

# Target: threenode - setup a three node cluster with console
threenode:
	make -e COMPOSE_PROFILES=$@ -e RP_VERSION=$(RP_VERSION)  $(UPDOWN) 

# Target: fournode - setup a four node cluster with console
fournode:
	make -e COMPOSE_PROFILES=$@ -e RP_VERSION=$(RP_VERSION)  $(UPDOWN) 

# Target: fivenode - setup a five node cluster with console
fivenode:
	make -e COMPOSE_PROFILES=$@ -e RP_VERSION=$(RP_VERSION)  $(UPDOWN) 

connect:
	make -e COMPOSE_PROFILES=$@ $(UPDOWN)

# Target: status - show running instances
status:
	@docker ps

shell:
	@docker exec -it redpanda-0 bash

up: 
	RP_VERSION=$(RP_VERSION) COMPOSE_FILE=$(COMPOSE_FILE) SEEDS=redpanda-0:33145 LOG_LEVEL=info COMPOSE_PROFILES=$(COMPOSE_PROFILES) docker compose up $(ARGS)

down:
	COMPOSE_FILE=$(COMPOSE_FILE) SEEDS=redpanda-0:33145 LOG_LEVEL=warn COMPOSE_PROFILES=$(COMPOSE_PROFILES) docker compose down

clean-images:
	docker image rm docker.redpanda.com/redpandadata/redpanda

# Target: clean - shutdown nodes and clean up/purge volumes -- WARNING: this is destructive
clean: COMPOSE_PROFILES=fivenode,connect
clean:
	make -e COMPOSE_PROFILES=fivenode,connect down
	#make -e COMPOSE_PROFILES=fivenode down
	docker ps -a --filter name=redpanda --format "{{.Names}}" | xargs docker rm -v
	COMPOSE_FILE=$(COMPOSE_FILE) SEEDS=redpanda-0:33145 LOG_LEVEL=warn COMPOSE_PROFILES=$(COMPOSE_PROFILES) docker volume prune -f
	docker volume ls --filter name=redpanda --format "{{.Name}}"| xargs docker volume rm -f
