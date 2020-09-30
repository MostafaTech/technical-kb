# Annotations
They are like labels but they can have longer values and you can't query by them.

Add annotations in yaml file:
```yaml
metadata:
  annotations:
    traefik.ingress.kubernetes.io/router.entrypoints: web
```