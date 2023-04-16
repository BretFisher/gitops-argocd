# Design 02

## Installing Argo

Assume the same `bootstrap` process as before, or Argo CD bootstrapping could be in another repo. This repo could just be for the app definitions.

## Telling Argo about each ApplicationSet on Day 1

```shell
kubectl apply -f .design-02/apps/root-applicationset.yaml
kubectl apply -f .design-02/apps/addons-applicationset.yaml
```

## Design 02, medium complexity

- Init each ApplicationSet above via `kubectl apply -f`
- Those Git Generators could monitor a subdir in this repository or a different repo
- Each apps environment override can live here or in another Kustomize/Helm repo
- Helm value files can live in a different HTTPS location than their chart
- Pro: Still not too complex
- Pro: Individual apps are auto-discovered unless a new repo needs to be watched
- Pro: For new apps or environments, only one PR is needed, and it doesn't have to be in this Argo CD repository
- Pro: Easier and more flexible to manage than app-of-apps pattern
- Con: Either Human or GHA needs to `kubectl apply -f` each app root on Day 1
