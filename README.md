[![Go Report Card](https://goreportcard.com/badge/github.com/kubevirt-ui/kube-gateway-operator)](https://goreportcard.com/report/github.com/kubevirt-ui/kube-gateway-operator)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

# kube-gateway-operator

![alt gopher network](https://raw.githubusercontent.com/kubevirt-ui/kube-gateway/main/docs/network-side.png)

kube-gateway-operator installs and operate [kube-gateway](https://github.com/kubevirt-ui/kube-gateway), kube-gateway allow access k8s API using time limited access tokens, kube-gateway allow usage of one time access tokens to k8s resources.

## Build and push images

```bash
export USERNAME=yaacov
IMG=quay.io/$USERNAME/kube-gateway-operator:v0.0.1 make podman-build
IMG=quay.io/$USERNAME/kube-gateway-operator:v0.0.1 make podman-push
```

## Deploy

```bash
# Deploy the operator, RBAC roles and CRDs
export USERNAME=yaacov
IMG=quay.io/$USERNAME/kube-gateway-operator:v0.0.1 make deploy

# Deploy from an example deployment yaml
# Will use pre-defined images and permistions, users can also copy this file to local
# directory and edit the container image used.
oc create -f https://raw.githubusercontent.com/kubevirt-ui/kube-gateway-operator/main/deploy/kube-gateway-operator.yaml
```

```bash
# Remove deployment of the operator, RBAC roles and CRDs
export USERNAME=yaacov
IMG=quay.io/$USERNAME/kube-gateway-operator:v0.0.1 make undeploy
```

## Create GateServer and GateToken examples

Example files:
[gateserver.yaml](/config/samples/kubegateway_v1beta1_gateserver.yaml),
[gatetoken.yaml](/config/samples/kubegateway_v1beta1_gatetoken.yaml)

```bash
# Use the kube-gateway namespace
oc create namespace kube-gateway

# create a sample gateway server
oc create -f config/samples/kubegateway_v1beta1_gateserver.yaml

# create a sample token request
oc create -f config/samples/kubegateway_v1beta1_gatetoken.yaml

# check the token
oc get gatetoken gatetoken-sample -o yaml
```

## Building for local development

```bash
# Compile operator
make

# Install CRD on cluser for running loaclly
make install
# make uninstall

# Run locally
make run
```

(gopher network image - [egonelbre/gophers](https://github.com/egonelbre/gophers))
