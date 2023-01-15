
build:
	docker compose -f ../docker-compose.yml build

remove-image:
	docker compose -f ../docker-compose.yml rm -sf

run :
	$(MAKE) run-detached
	$(MAKE) provision
	docker compose -f ../docker-compose.yml logs -f web worker

run-detached:
	docker compose -f ../docker-compose.yml up -d web worker

provision:
	docker compose -f ../docker-compose.yml run --no-deps provision python3 -m boptest_submit --shared --path ./boptest/testcases/${TESTCASE}

stop:
	docker compose -f ../docker-compose.yml down

.PHONY: build run run-detached remove-image stop provision
