# Demo of Argo CD ApplicationSet Controller

This repository contains example configuration for deploying
Argo CD Applications with [ApplicationSet Controller](https://argocd-applicationset.readthedocs.io/en/stable/).

## Deploying the example

### Pre-requisites

1. Kubernetes cluster with `argocd` namespace.
2. Argo CD deployed in `argocd` namespace. Quick deploy: `helm upgrade --install argocd-demo argo/argo-cd -n argocd`
3. Argo CD ApplicationSet Controller deployed in `argocd` namespace. Quick deploy: `helm upgrade --install argocd-appset-demo argo/argocd-applicationset -n argocd`

### Deploy Top-Level Application

Clone the repository and run below command in root of the repository. 
This will deploy an Application which will deploy the ApplicationSet 
resource which will end up deploying two "tenant" Applications.

```shell
kubectl apply -f top-level-app/TopLevelApplication.yaml -n argocd
```

Eventually, all applications will get deployed and the Argo CD home page should look like this:

![image](https://user-images.githubusercontent.com/4991449/135903301-9085dd5f-bcd6-4e57-8fdf-59b81745fbee.png)

The ApplicationSet deploys two "tenant" apps which are actually Wordpress installation with different `values.yaml` for each tenant.

<p>
  <img src="https://user-images.githubusercontent.com/4991449/135905713-c84f0b10-aed7-4b6c-b3a2-8c7bd7b6b5c5.png" width="480" />
  <img src="https://user-images.githubusercontent.com/4991449/135905746-485a8091-a9da-49e3-ad8e-fc46d82137f0.png" width="480" />
</p>

The ApplicationSet is deployed using the [Git Files Generator](https://argocd-applicationset.readthedocs.io/en/stable/Generators-Git/#git-generator-files).

Please read the [accompanying blog](https://itnext.io/level-up-your-argo-cd-game-with-applicationset-ccd874977c4c) for further explanation.
