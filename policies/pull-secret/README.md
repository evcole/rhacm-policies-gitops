# Global pull-secret management

This policy provides automation for managing the content of the global OpenShift pull secret across managed clusters.

## Prerequisites
* A RHACM hub cluster
* A secret `global-pull-secret-merge-source` in the `pull-secret-importer` namespace, containing valid .dockerconfigjson base64-encoded auths

## Design

The policy functions by looking up an existing secret, decoding its auth content, and merging it into the contents of the global pull-secret.

Using this policy, a "source-of-truth" secret can be defined on the local cluster, enforcing its content must be present in `openshift-config/pull-secret`.

This is valuable in instances such as newly deployed Azure Red Hat OpenShift (ARO) clusters. The `cloud.openshift.com` pull-secret is stripped out of the global secret upon cluster provisioning, requiring manual replacement. Additionally, the internal Azure Container Registry (ACR) pull-secret entry is generated (arosvc.azurecr.io), which must not be touched as the cluster relies upon the global system image registry. This policy automates the process when enforced.

Unique entries from both the imported secret and global pull-secret are kept. Matching registry entries will be overwritten, keeping the content of the imported secret. 
