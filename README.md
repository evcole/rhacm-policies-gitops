# RHACM Policies

This repository provides out-of-the-box automation for continuous delivery of RHACM policies to a hub cluster using OpenShift GitOps.

## Prerequisites
* A RHACM hub cluster
* OpenShift GitOps installed (ArgoCD)

## Setup

1. Clone the repository  
`git clone https://github.com/evcole/rhacm-policies-gitops.git`
2. Patch the ArgoCD instance to include the kustomize plugin definitions and RHACM image tag
See the [Integrating Policy Generator documentation](https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_management_for_kubernetes/2.17/html/gitops/gitops-overview#integrate-pol-gen-ocp-gitops)  
3. Create the ArgoCD application  
`oc apply -f bootstrap/application.yaml`
4. Verify the application was created successfully  
`oc get applications.argoproj.io rhacm-policies -n openshift-gitops`  
`oc describe applications.argoproj.io rhacm-policies -n openshift-gitops`
