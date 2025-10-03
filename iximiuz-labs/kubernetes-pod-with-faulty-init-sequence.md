# Kubernetes Pod With a Faulty Init Sequence
https://labs.iximiuz.com/challenges/kubernetes-pod-with-faulty-init-sequence

Issue: The sidecar container "announcer" cant to connect to "identity-provider" container. So, inspect the yaml of the pod

```bash
kubectl get pod faulty -n challenge -oyaml > pod.yaml
```

Delete generated info like status, created time, annotation to get appliable manifest.

Put the identity-provider container spec under initContainers
Because of the "announcer" depends to "identity-provider", add `restartPolicy: Always` to announcer.

After that, delete the pod and re-apply new configuration

```bash
kubectl delete pod faulty -n challenge --force
kubectl apply -f pod.yaml
```
