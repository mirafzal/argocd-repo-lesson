# argocd-repo-lesson

1. Install ArgoCD with helm:
```
helm install -n argocd argocd argocd/argo-cd --version 8.5.0 --create-namespace
```

2. Get ArgoCD admin password:
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

3. Apply app-of-apps:
```
kubectl apply -f argocd/app-of-apps.yaml
```

4. Port-forward argocd web UI:
```
kubectl port-forward service/argocd-server -n argocd 8080:443
```

---
Test celery tasks:
```
k -n mydjangoapp exec -it mydjangoapp-celery-77fcfb88bc-scblz -- sh
```
```
python manage.py shell
```
```
from mydjangoapp.celery import long_task
for i in range(100):
    long_task.delay()
```