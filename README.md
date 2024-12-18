# GitOps IaC designs for Argo CD

This repository contains a set of GitOps infrastructure-as-code designs for Argo CD. Three designs that grow in complexity (as well as feature set) are in this repositories `design` directories.

## Design 1: Simple start

[`design-01`](./design-01/) Only uses `Application` resources. While simpler to understand and implement, this design requires PRs for each new app to be "watched" by Argo CD.

## Design 2: Application Sets

[`design-02`](./design-02/) This design uses `ApplicationSet` to watch a group of apps via a single `kubectl apply`. This is a good enhancement over `design-01` because it reduces the number of PRs needed to add a new app or environment. No real downsides once you understand both `Application` and `ApplicationSet` resources.

## Design 3: Argo CD Autopilot

[`design-03`](./design-03/) This design uses [Argo CD Autopilot](https://github.com/argoproj-labs/argocd-autopilot) to manage Argo CD itself, as well as the namespaces and Application Sets. Everything but a single `kubectl apply` is automated by Argo CD. The repo and YAML relationships are more complex, and introduces `AppProject` and additional JSON files. This design is the most complex, but also the most powerful.
