# argo sample structure layout

the funny thing here is i've just basically gotten a self-hosted single tenant akuity platform thing going

root app yaml - sources are itself and the appsets folder - rewrite here
appsets - everything gets an appset even single cluster apps - rewrite here
apps - contains helm values, kustomize manifests for extra resources (external secrets, etc)

## notes on kargo

clusterpromotiontask to do the usual things

pre-update-image:
* git-clone
* git-clear

in your repo's stages:
* kustomize-set-image - as many times as needed for as many sidecars and stuff

post-update-image:
* kustomize-build
* github-push
* compose-output - build argocd app name
* argocd-update
* argocd-wait - watch the timeout if we have a long canary process or run validation tests in the canary!

### gha-dispatch

this is enterprise stuff on akuity

just grab a container with the gh cli, do like `gh workflow dispatch` and `gh workflow wait`

## other things i like

* external-secrets
* external-dns
* argo-rollouts
* keda
* kube-state-metrics
* kyverno
* metrics-server
* falco
* perfectscale (saas)
* renovatebot (self hosted)

## ci patterns

push an image, this kicks off kargo when a matching image and commit exist

### merge queue optional

kargo posts back github status checks using the http action
use external secrets to make github tokens we can pass in via a sharedSecret

can post on success or failure

## everything else

cloud specific and customer specific
stuff like karpenter configs if on aws, or the argo rollouts readiness gate
or how to discover microservices if we want to fan out autodiscover them, that's all company specific concerns
