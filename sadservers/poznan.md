https://sadservers.com/newserver/poznan

```bash
sed -i '/protocol: TCP/a\
          volumeMounts:\
            - name: html\
              mountPath: /usr/share/nginx/html\
      volumes:\
        - name: html\
          configMap:\
            name: {{ .Release.Name }}-cm-index-html' \
    templates/deployment.yaml
sed -i 's/replicaCount: 3/replicaCount: 1/' values.yaml
helm upgrade --install web-chart -f values.yaml .
```