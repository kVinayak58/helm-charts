# helm-charts

Kubernetes Helm charts for ShopEasy microservices.

## Layout

```
helm-charts/
├── charts/microservice/   # Generic chart (Deployment, Service, Ingress)
├── values-dev.yaml        # namespace: shopeasy-dev
├── values-qa.yaml
├── values-uat.yaml
└── values-prod.yaml
```

## BOMP digest deploy

```bash
helm upgrade --install product-service charts/microservice \
  -f values-prod.yaml \
  --set name=product-service \
  --set image.repository=267423569109.dkr.ecr.us-east-1.amazonaws.com/shopeasy-product-service \
  --set image.tag=2.4.1-a1b2c3d \
  --set image.digest=sha256:abc123... \
  --namespace shopeasy-prod
```

When `image.digest` is set, Kubernetes pulls by digest — tag is audit-only.

## Rollback

```bash
helm rollback product-service 13 -n shopeasy-prod --wait
```
