# Pods:
- Pods are the smallest deployable units in Kubernetes.
- A Pod is a group of one or more containers, with shared storage and network resources.

## write simple manifest file to create pod:
```
vim simple-pod.yaml
```
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
```
```
kubectl apply -f simple-pod.yaml
```
```
kubectl get pod
```
```
kubectl describe pod <pod-name>
```
