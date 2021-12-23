
# VARIABLES

DOCKER_REGISTRY = index.docker.io
IMAGE_NAME = debian
IMAGE_VERSION = 11
IMAGE_ORG = marcelofpfelix

# Generated variables
IMAGE_TAG = $(DOCKER_REGISTRY)/$(IMAGE_ORG)/$(IMAGE_NAME):$(IMAGE_VERSION)
WORKING_DIR := $(shell pwd)
docker_build_args = --build-arg GIT_COMMIT=$(shell git show -s --format=%H) --build-arg GIT_COMMIT_DATE="$(shell git show -s --format=%ci)"


.DEFAULT_GOAL := build
.PHONY: build


# TARGETS

all: build push 

clean:
	@echo removing $(IMAGE_TAG)
	-docker rmi -f $(IMAGE_TAG)

build:
	@echo building $(IMAGE_TAG)
	@docker build $(docker_build_args) -t $(IMAGE_TAG) $(WORKING_DIR)

push:
	@echo pushing $(IMAGE_TAG)
	@docker push $(IMAGE_TAG)

run::
	@echo running $(IMAGE_TAG)
	@docker run -it \
		$(DOCKER_REGISTRY)/$(IMAGE_ORG)/$(IMAGE_NAME):$(IMAGE_VERSION)
	@docker run -it \
		$(DOCKER_REGISTRY)/$(IMAGE_ORG)/$(IMAGE_NAME):latest