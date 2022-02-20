# VARIABLES
IMAGE_NAME = debian
IMAGE_VERSION = 10-se

DOCKER_REGISTRY = index.docker.io
IMAGE_ORG = marcelofpfelix
INTERNAL_REGISTRY = registry.docker.internal.bandonga.com
INTERNAL_ORG = library

# Generated variables
IMAGE_TAG = $(DOCKER_REGISTRY)/$(IMAGE_ORG)/$(IMAGE_NAME):$(IMAGE_VERSION)
IT_L = $(DOCKER_REGISTRY)/$(IMAGE_ORG)/$(IMAGE_NAME):latest
IT_I = $(INTERNAL_REGISTRY)/$(INTERNAL_ORG)/$(IMAGE_NAME):$(IMAGE_VERSION)
IT_IL = $(INTERNAL_REGISTRY)/$(INTERNAL_ORG)/$(IMAGE_NAME):latest

WORKING_DIR := $(shell pwd)
docker_build_args = --build-arg GIT_COMMIT=$(shell git show -s --format=%H) --build-arg GIT_COMMIT_DATE="$(shell git show -s --format=%ci)"


.DEFAULT_GOAL := build
.PHONY: build


# TARGETS

all: build push 

clean:
	@echo MAKE removing $(IMAGE_TAG)
	-docker rmi -f $(IMAGE_TAG)

build:
	@echo building $(IMAGE_TAG)
	@docker build $(docker_build_args) -t $(IMAGE_TAG) $(WORKING_DIR)

test:
	@echo MAKE testing $(IMAGE_TAG)
	@trivy image --ignore-unfixed --exit-code 1 --severity CRITICAL $(IMAGE_TAG)

hub:
	@echo MAKE pushing $(IMAGE_TAG)
	@docker push $(IMAGE_TAG)

push:
	@echo MAKE pushing $(IT_I)
	@docker tag $(IMAGE_TAG) $(IT_I)
	@docker push $(IT_I)

run::
	@echo running $(IMAGE_TAG)
	@docker run -dit --rm --name $(IMAGE_NAME) \
		$(DOCKER_REGISTRY)/$(IMAGE_ORG)/$(IMAGE_NAME):$(IMAGE_VERSION)