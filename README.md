# RHACM Policies

This repository provides out-of-the-box automation for continuous delivery of RHACM policies to a hub cluster using OpenShift GitOps.

## Prerequisites
* A RHACM hub cluster
* OpenShift GitOps installed (ArgoCD)

## Setup

1. Clone the repository
`git clone https://github.com/evcole/rhacm-policies-gitops.git`
2. Apply the application manifest
`cd pull-secret-manager`
`oc apply -f bootstrap/application.yaml`
