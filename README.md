# helm-kubernetes Docker hub image

[![ci](https://github.com/prajinults/helm-kubectl-skopeo/actions/workflows/image-build-push.yaml/badge.svg)](https://github.com/prajinults/helm-kubectl-skopeo/actions/workflows/image-build-push.yaml)
[![Docker Stars](https://img.shields.io/docker/stars/prajinults/helm-kubectl-skopeo.svg?style=flat)](https://hub.docker.com/r/prajinults/helm-kubectl-skopeo/)
[![Docker Pulls](https://img.shields.io/docker/pulls/prajinults/helm-kubectl-skopeo.svg?style=flat)](https://hub.docker.com/r/prajinults/helm-kubectl-skopeo/)

Supported tags and release links

* [3.14.4](https://github.com/prajinults/helm-kubectl-skopeo/releases/tag/3.14.4) - helm v3.14.4, kubectl v1.29.3, alpine 3.19

## Overview

This lightweight alpine docker image provides kubectl helm and skopeo binaries for working with a Kubernetes cluster. A local configured kubectl is a prerequisite to use helm per [helm documentation](https://github.com/kubernetes/helm/blob/master/docs/quickstart.md). This image is useful for general helm administration such as deploying helm charts and managing releases. It is also perfect for any automated deployment pipeline needing to use helm which supports docker images such as [Concourse CI](https://concourse.ci), [Jenkins on Kubernetes](https://kubeapps.com/charts/stable/jenkins), [Travis CI](https://docs.travis-ci.com/user/docker/), and [Circle CI](https://circleci.com/integrations/docker/). Having bash installed allows for better support for troubleshooting by being able to exec / terminal in and run desired shell scripts. Git installed allows installation of [helm plugins](https://github.com/kubernetes/helm/blob/master/docs/plugins.md).

If it is desired to only use kubectl and have kubectl as the entry command (versus this image as bash entry command), I recommend checking out this image instead:
[lachlanevenson/kubectl](https://hub.docker.com/r/lachlanevenson/k8s-kubectl/)

## Run

Example to just run helm on entry:  
`docker run --rm prajinults/helm-kubectl-skopeo helm`  
By default kubectl will try to use /root/.kube/config file for connection to the kubernetes cluster, but does not exist by default in the image.

Example for use with personal administration or troubleshooting with volume mount for kubeconfig files:  
`docker run -it -v ~/.kube:/root/.kube prajinults/helm-kubectl-skopeo`  
The -v maps your host docker machine Kubernetes configuration directory (~/.kube) to the container's Kubernetes configuration directory (root/.kube).

## Build

For doing a manual local build of the image:  
`make docker_build`
