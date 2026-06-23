# RHACM Policies

This repository provides out-of-the-box automation for continuous delivery of RHACM policies to a hub cluster using OpenShift GitOps.

## Prerequisites
* A RHACM hub cluster
* OpenShift GitOps installed (ArgoCD)

## Setup

1. Clone the repository  
`git clone https://github.com/evcole/rhacm-policies-gitops.git`
2. Patch the ArgoCD instance to include the kustomize plugin definitions and RHACM image tag
3. Grant ArgoCD the necessary permissions to manage RHACM policies  
`cd rhacm-policies-gitops`  
`oc apply -f infra/clusterrole.yaml`  
`oc apply -f infra/clusterrolebinding.yaml`  
4. Create the ArgoCD application  
`oc apply -f bootstrap/application.yaml`
5. Verify the application was created successfully  
`oc get applications.argoproj.io rhacm-policies -n openshift-gitops`  
`oc describe applications.argoproj.io rhacm-policies -n openshift-gitops`
