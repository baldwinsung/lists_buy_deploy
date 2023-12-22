# lists_buy_deploy

lists_buy_deploy



## Deploy to Kubernetes

### Create secret in Kubernetes for pulling image from ghcr

```
GH_USERNAME="github_username"
GKEY="github_classic_api_key"
GH_EMAIL="user@somedomain"
kubectl create secret docker-registry ghcr-login-secret --docker-server=https://ghcr.io --docker-username=$GH_USERNAME --docker-password=$GKEY --docker-email=$GH_EMAIL
```

### 

## Deploy using kubectl apply

### Deploy

```
kubectl apply -f deploy.yaml
kubectl get pods
```

### Service

```
kubectl apply -f service.yaml
kubectl get service
```

### Ingress

```
kubectl apply -f ingress.yaml
kubectl get ingress
```



## Verification
Verify via the Ingress. Add an IP and the host record to /etc/hosts.

```
kubectl get ingress | grep traefik | awk '{print $4" "$3}' | cut -d, -f3
curl http://buy.test.local
```

## Debugging
For purposes of debugging. You can verify by using port-forward to access to the pod and/or service directly.

### pod
```
PF_POD="`kubectl get pod | grep Running | head -1 | awk '{print $1}'`"
kubectl port-forward pod/${PF_POD} 8888:8888
curl http://localhost:8888
```

### service
```
kubectl port-forward service:buy 8888:8888
curl http://localhost:8888
```

