DB=enceladus
BUILD=${CURDIR}/build.sql
SCRIPTS=${CURDIR}/scripts
CSV='${CURDIR}/../data/master_plan.csv'
MASTER=$(SCRIPTS)/import.sql
NORMALIZE = $(SCRIPTS)/normalize.sql 
CURDATE=$(shell date -u '+%Y-%m-%d %H:%M:%S UTC')
NAME=$(shell basename `pwd`)

all: normalize
	psql $(DB) -f $(BUILD)

master: start_build
	@cat $(MASTER) >> $(BUILD)

import: master
	@echo "COPY import.master_plan FROM $(CSV) WITH DELIMITER ',' HEADER CSV;" >> $(BUILD)

normalize: import
	@cat $(NORMALIZE) >> $(BUILD)

start_build:
	@echo "-- $(CURDATE): build file curious-moon/$(NAME)" > $(BUILD)

clean:
	@rm -rf $(BUILD)
