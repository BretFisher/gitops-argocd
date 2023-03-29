# gitops-argocd

## Installing Argo

```shell
kubectl apply -k ./bootstrap
sleep 60
argocd admin initial-password -n argocd
```

## Telling Argo about each app

```shell
kubectl apply -f ./apps/wordsmith-staging01.yaml
```

## Design 01, the simplest setup

- Init Argo CD via `kubectl apply -k`
- Init each app via `kubectl apply -f`
- Single project with all apps (just fine for small team self-managed)
- Each apps environment overrides can live here or in their Kustomize/Helm repo
- Pro: So simple anyone can do it
- Pro: All overrides are kept in Kustomize/Helm elsewhere, so Argo CD isn't needed for test/dev
- Pro: Once app is added here, all further app updates happen in their Kustomize/Helm repo
- Con: Either Human or GHA needs to `kubectl apply -f` each app once
- Con: For new apps or environments, two PRs are needed if env overrides are elsewhere
