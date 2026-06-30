# RHACM Policies

This repository provides out-of-the-box automation for continuous delivery of RHACM policies to a hub cluster using OpenShift GitOps.

## Prerequisites
* A RHACM hub cluster

## Setup

1. Clone the repository  
`git clone https://github.com/evcole/rhacm-policies-gitops.git`  
`cd rhacm-policies-gitops`  
2. Apply the bootstrap manifests  
`oc apply -k bootstrap/`  
See the [Integrating Policy Generator documentation](https://docs.redhat.com/en/documentation/red_hat_advanced_cluster_management_for_kubernetes/2.17/html/gitops/gitops-overview#integrate-pol-gen-ocp-gitops)  
3. Apply the ArgoCD manifests  
`oc apply -k gitops/`  
It may be necessary to restart the OpenShift GitOps resources:  
`oc rollout restart deploy/openshift-gitops-repo-server -n openshift-gitops`  
4. Verify ArgoCD is deployed and the application was created successfully  
`oc get pods -n openshift-gitops`  
`oc get applications.argoproj.io rhacm-policies -n openshift-gitops`  
`oc describe applications.argoproj.io rhacm-policies -n openshift-gitops` 

## Policies

If configured properly, the `rhacm-policies` Argo application will deliver the policies to the hub cluster. To add new policies, simply create a new directory under policies/ and add the requisite manifests. If using Policy Generator, be sure to add the path entry to the `generators` in `policies/kustomization.yaml`. If using generic policies, add to the `resources` in `policies/kustomization.yaml`.  
