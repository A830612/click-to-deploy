include ../crd.Makefile
include ../gcloud.Makefile
include ../var.Makefile
include ../images.Makefile

APP_ID ?= consul

SOURCE_REGISTRY ?= marketplace.gcr.io/google

TRACK ?= 1.4
METRICS_EXPORTER_TAG ?= v0.5.1

# List of images used in application
TARGET_IMAGES := consul-exporter prometheus-to-sd

# Image variable names should correspond with TARGET_IMAGES list
image-$(APP_ID) := $(call get_sha256,$(SOURCE_REGISTRY)/consul1:$(TRACK))
image-consul-exporter := $(call get_sha256,$(SOURCE_REGISTRY)/consul1:exporter)
image-prometheus-to-sd := $(call get_sha256,k8s.gcr.io/prometheus-to-sd:$(METRICS_EXPORTER_TAG))

# TODO(aav66): Replace with C2D_RELEASE variable after container is updated.
C2D_CONTAINER_RELEASE := $(call get_var_from_container,$(image-$(APP_ID)),CONSUL_VERSION)

BUILD_ID := $(shell date --utc +%Y%m%d-%H%M%S)
RELEASE ?= $(C2D_CONTAINER_RELEASE)-$(BUILD_ID)

NAME ?= $(APP_ID)-1

APP_PARAMETERS ?= { \
  "name": "$(NAME)", \
  "namespace": "$(NAMESPACE)" \
}

# c2d_deployer.Makefile provides the main targets for installing the application.
# It requires several APP_* variables defined above, and thus must be included after.
include ../c2d_deployer.Makefile
