https://sadservers.com/newserver/ruaka

```bash
echo '''
spec:
  template:
    spec:
      containers:
      - name: ruaka
        startupProbe:
          httpGet:
            path: /
            port: http
            scheme: HTTP
          failureThreshold: 12
          periodSeconds: 5
          timeoutSeconds: 5''' > patch.yaml
kubectl apply -f patch.yaml
kubectl rollout restart deploy ruaka
```
