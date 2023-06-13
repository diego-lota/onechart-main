# Onechart
This repo contains the Argo CD `ApplicationSet` resource manifests to bootstrap the cluster with all apps and resources, as well as necessary manifests which each application uses.

## Applications
### Cluster Resources
These are 3rd-party apps which add supporting functionality.

#### [Ambassador Edge Stack](https://www.getambassador.io/docs/edge-stack/)
Ambassador is the API gateway for all requests into the stack. It provisions the AWS loadbalancer and routes traffic to all other apps.

#### [Argo CD](https://argo-cd.readthedocs.io/en/stable/)
The resource manifests necessary for Ambassador to route requests for the Argo CD UI are stored here.

#### [Cert-Manager]( https://cert-manager.io/)
Cert-manager creates a [`ClusterIssuer`](https://cert-manager.io/docs/concepts/issuer/) resource which provides apps the ability to generate TLS certificates.

#### [ExternalDNS](https://kubernetes-sigs.github.io/external-dns/v0.12.2/)
The ExternalDNS deployment handles creation of CloudFlare DNS records which point to the loadbalancer configured by Ambassador. It functions by watching Ambassador [`Host` resources](https://www.getambassador.io/docs/edge-stack/latest/topics/running/host-crd/) and looking for the [`external-dns.ambassador-service`](https://www.getambassador.io/docs/edge-stack/2.1/howtos/external-dns/) annotation which specifies which service in the kubernetes cluster which is configured to handle requests.

#### [Ory Kratos](https://www.ory.sh/docs/kratos/ory-kratos-intro)
Ory Identities (Ory Kratos) is an API-first identity and user management system built following [cloud architecture best practices](https://www.ory.sh/docs/ecosystem/software-architecture-philosophy). It implements mechanisms that allow handling core use cases that the majority of modern software applications have to deal with.

##### Note:
To log in using the ArgoCD CLI and for all further `argocd` CLI commands, add `--port-forward-namespace argocd` as a command line argument
```
argocd login --username admin --password admin argocd-uat.eddanileyko.com --port-forward-namespace argocd
```