# 🦀 refactored-adventure 🦀

A repository that contains kustomize (or other) config for use by ci-cd tooling in [ubiquitous-journey](https://github.com/rht-labs/ubiquitous-journey)

## Applications

Kustomize has the concept of `base` and `overlays`. Overlays can be used to model environments e.g. overlays/{dev,staging,prod}/kustomization.yaml

You can deploy the applications using argocd cli directly but more commonly they are deployed as part of a helm chart from the ubiquitous-journey project.

### Code Ready Workspaces

`crw`
```
argocd repo add https://github.com/rht-labs/refactored-adventure.git
argocd app create crw \
  --repo https://github.com/rht-labs/refactored-adventure.git \
  --path crw/base \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace crw \
  --revision master \
  --sync-policy automated

# TODO deleting the argocd project and operator may hang, to fix
oc patch checluster.org.eclipse.che codeready-workspaces -n crw --type='json' -p='[{"op": "replace", "path": "/metadata/finalizers", "value":[]}]'
```

`tekton`
```
argocd repo add https://github.com/rht-labs/refactored-adventure.git
argocd app create tekton \
  --repo https://github.com/rht-labs/refactored-adventure.git \
  --path tekton/base \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace openshift-operators \
  --revision master \
  --sync-policy automated
```

`cert-utils`
```
argocd repo add https://github.com/rht-labs/refactored-adventure.git
argocd app create cert-utils \
  --repo https://github.com/rht-labs/refactored-adventure.git \
  --path cert-utils/base \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace openshift-operators \
  --revision master \
  --sync-policy automated
```

`knative`
```
argocd repo add https://github.com/rht-labs/refactored-adventure.git
argocd app create knative \
  --repo https://github.com/rht-labs/refactored-adventure.git \
  --path knative/base \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace openshift-serverless \
  --revision master \
  --sync-policy automated
```

`container-security-operator`
```
argocd repo add https://github.com/rht-labs/refactored-adventure.git
argocd app create container-security-operator \
  --repo https://github.com/rht-labs/refactored-adventure.git \
  --path container-security-operator/base \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace openshift-operators \
  --revision master \
  --sync-policy automated
```

`user-workload-monitoring`
```
argocd repo add https://github.com/rht-labs/refactored-adventure.git
argocd app create user-workload-monitoring \
  --repo https://github.com/rht-labs/refactored-adventure.git \
  --path user-workload-monitoring/base \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace openshift-monitoring \
  --revision master \
  --sync-policy automated
```

`amq-streams`
```
argocd repo add https://github.com/rht-labs/refactored-adventure.git
argocd app create amq-streams \
  --repo https://github.com/rht-labs/refactored-adventure.git \
  --path amq-streams/base \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace strimzi \
  --revision master \
  --sync-policy automated
```

`istio`
```
argocd repo add https://github.com/rht-labs/refactored-adventure.git
argocd app create istio \
  --repo https://github.com/rht-labs/refactored-adventure.git \
  --path istio/istio-system \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace openshift-operators \
  --revision master \
  --sync-policy automated
```

`elastic`
```
argocd repo add https://github.com/rht-labs/refactored-adventure.git
argocd app create elastic \
  --repo https://github.com/rht-labs/refactored-adventure.git \
  --path elastic/base \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace openshift-operators \
  --revision master \
  --sync-policy automated
```

`microcks`
```
argocd repo add https://github.com/fmenesesg/refactored-adventure.git
argocd app create microcks \
  --repo https://github.com/fmenesesg/refactored-adventure.git \
  --path microcks/base \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace microcks \
  --revision master \
  --sync-policy automated
```