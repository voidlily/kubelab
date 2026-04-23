# argo sample structure layout

root app yaml - defines itself, defines appsets
appsets - everything gets an appset even single cluster apps
apps - contains helm values, kustomize manifests for extra resources (external secrets, etc)
