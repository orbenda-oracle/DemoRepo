# nginx-demo Helm Chart

A minimal Helm chart to deploy NGINX servers.

## Install

```bash
helm install my-nginx ./helm/nginx
```

## Values

- **replicaCount**: number of replicas (default 2)
- **image.repository**: container image (default `nginx`)
- **image.tag**: image tag (default chart appVersion)
- **service.type**: `ClusterIP`, `NodePort`, or `LoadBalancer`
- **service.port**: service port (default 80)
- **ingress.enabled**: enable ingress
- **ingress.className**: ingress class
- **ingress.hosts**: list of hosts and paths

## Example with Ingress

```bash
helm install my-nginx ./helm/nginx \
  --set ingress.enabled=true \
  --set ingress.className=nginx \
  --set ingress.hosts[0].host=example.local \
  --set ingress.hosts[0].paths[0].path=/ \
  --set ingress.hosts[0].paths[0].pathType=Prefix
```

## Uninstall

```bash
helm uninstall my-nginx
```

## Oracle Cloud OKE

For OKE with an OCI Load Balancer, use the provided overrides:

```bash
helm install my-nginx ./helm/nginx -f ./helm/nginx/values-oke.yaml
```

Key Service annotations used in `values-oke.yaml`:

- `service.beta.kubernetes.io/oci-load-balancer-shape: "flexible"`
- `service.beta.kubernetes.io/oci-load-balancer-shape-flex-min: "10"`
- `service.beta.kubernetes.io/oci-load-balancer-shape-flex-max: "10"`
- `service.beta.kubernetes.io/oci-load-balancer-preserve-source: "true"`
- optional subnets: `service.beta.kubernetes.io/oci-load-balancer-subnet1`, `...-subnet2`

If you need to restrict source IPs, set `service.loadBalancerSourceRanges`.
