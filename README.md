# Global pull-secret management using RHACM PolicyGenerator and ExternalSecrets

This policy provides automation for managing the content of the global OpenShift pull secret across managed clusters.
The policy looks up and decodes an existing secret on the cluster, then merges them into the cluster-wide pull-secret in `openshift-config`. Unique entries from either secret are kept. Matching entries will be overwritten, keeping the content of the imported secret.  

## Prerequisites
* A RHACM hub cluster
* OpenShift GitOps installed (ArgoCD)

## Setup

1. Clone the repository
`git clone https://github.com/evcole/pull-secret-manager.git`
2. Apply the application manifest
`cd pull-secret-manager`
`oc apply -f bootstrap/application.yaml`

