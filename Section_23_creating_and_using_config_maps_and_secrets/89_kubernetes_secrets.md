# Kubernetes Secrets

## Password, tokens, sensitive information
- for sensitive infromation there is another special resource: Secrets
- Secrets and Configmaps work almost the same way
  - we will expose the differences on the next slide
- the intent is different thought
  - you should use secrets for things which are actually secret like API keys, credentials, etc. and use config map for not-secrtet configuratiuon data
  - in the future there will likely be some differentiators for secrets like roation or support for backing the secrtet api w/ HSMs etc


## Differences between ConfigMaps and Secrets

- secrets are base64-encoded when shown with `kubectl get secrets -o yaml`
  -  keep in mind that this is just encoding not encryption
  -  it is very easy to automatically extract and decode secrets
- secters can be encrypted at rest
- wiith rbac we can authorize a user to access ConfigMaps, but not Secrets 
  - since they are two different kinds of resources

# LINKS
https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/
https://kubernetes.io/docs/concepts/configuration/secret/
