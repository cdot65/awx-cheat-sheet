# Ansible Tower AWX cheat sheet

## setting up Ansible AWX with Rancher k3s

setup steps

``` bash
curl -sfL https://get.k3s.io | sudo bash -
kubectl get nodes
kubectl version --short
kubectl apply -f https://raw.githubusercontent.com/ansible/awx-operator/0.13.0/deploy/awx-operator.yaml
kubectl get pods
kubectl logs -f awx-operator-69c646c48f-f8ggg

vim awx.yaml

kubectl apply -f awx.yaml
kubectl get pods -A
kubectl logs -f awx-operator-69c646c48f-f8ggg
kubectl get pods -l "app.kubernetes.io/managed-by=awx-operator"
kubectl get svc
kubectl get secret
kubectl get secret awx1-admin-password -o jsonpath="{.data.password}" | base64 --decode
kubectl logs -f awx1-767c7b995c-69vh5 -c awx1-web
kubectl exec -it awx1-767c7b995c-69vh5 -c awx1-web -- bash
```

## awx.yaml 

```yaml
---
apiVersion: awx.ansible.com/v1beta1
kind: AWX
metadata:
  name: awx1
spec:
  service_type: nodeport
  ingress_type: none
  hostname: awx1.dmz.home
```

## setting up AWX

### User buildout

1. Create Organization
2. Create User
3. Create Teams
4. Associate User to Team / etc.

### Credientials

1. Network Login for AWX
2. SCM login
