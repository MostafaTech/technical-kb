# Services

## Sample Service file
```yaml
apiVersion: v1
kind: Service
metadata:
  name: vuecon-iran-service
spec:
  selector:
    app: vuecon-iran
  type: NodePort
  ports:
  - port: 80
    nodePort: 30080
```