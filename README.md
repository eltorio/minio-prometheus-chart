# minio-prometheus-chart
A Minio® Helm chart embedding a minimalistic Prometheus container
```sh
helm repo add highcanfly https://helm-repo.hyghcanfly.club/
helm repo update highcanfly
helm upgrade --install --namespace=sandbox-minio --create-namespace --values values.yaml minio highcanfly/minio
```

## Sample values.yaml
```yaml
minio:
  rootUser: administrator
  rootPassword: goodPassword
  replicas: 8
  ingress:
    annotations:
      cert-manager.io/cluster-issuer: letsencrypt-issuer
    enabled: true
    hosts:
      - minio.example.org
    tls:
    - secretName: minio.example.org-tls
      hosts:
        - minio.example.org
  consoleIngress:
    annotations:
      cert-manager.io/cluster-issuer: letsencrypt-issuer
    enabled: true
    hosts:
      - minio-console.example.org
    tls:
    - secretName: minio-console.example.org-tls
      hosts:
        - minio-console.example.org
  persistence:
    size: 10Gi 
  environment:
    MINIO_BROWSER_REDIRECT_URL: https://minio-console.example.org
    MINIO_SERVER_URL: https://minio.example.org

```
