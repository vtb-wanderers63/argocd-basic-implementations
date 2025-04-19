Syncing an App:

```
kubectl patch application <application-name> -n argocd --type merge -p '{"operation": {"sync": {}}}'
```

Check sync status:

get operation State:

```
kubectl get application nodejs-express-app -n argocd -o json | jq '.status.operationState'
```

Sync Status:
```
kubectl get application nodejs-express-app -n argocd \
  -o=jsonpath='{.status.sync.status}'
```

Health Status 
```
kubectl get application nodejs-express-app -n argocd \
  -o=jsonpath='{.status.health.status}'
```

Check whether the app was synced 
- check the latest commit sha:
```
git rev-parse origin/master
```

- if not synced. run sync


Check whether the pipeline was synced:

- compare repo to tekton middleware
