# Kubernetes Stateful Applications

### Stateful Applications
Stateful applications save data to some form of storage that remains consistent across restarts. Examples include databases like MySQL and PostgreSQL.

### StatefulSets
StatefulSets are a Kubernetes resource used to manage stateful applications. They provide guarantees about the ordering and uniqueness of pods.

#### Key Features of StatefulSets
- **Stable Network Identities:** Each pod in a StatefulSet gets a unique and stable network identity, which helps in maintaining the state.
- **Stable Storage:** Each pod can have its own persistent volume, which remains the same even if the pod is rescheduled.
- **Ordered Deployment and Scaling:** Pods are created, deleted, and scaled in an ordered sequence, ensuring proper initialization and termination.
- **Ordered Rolling Updates:** Updates to the pods occur in a controlled manner, one at a time, to maintain application availability.

### Persistent Volumes (PV) and Persistent Volume Claims (PVC)
StatefulSets typically use Persistent Volumes (PVs) and Persistent Volume Claims (PVCs) to provide stable storage.

- **Persistent Volumes (PV):** A piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes.
- **Persistent Volume Claims (PVC):** A request for storage by a user. Pods use PVCs to request PVs.

## Example of a StatefulSet with Persistent Storage

### Persistent Volume Claim

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi

```


StatefulSet
```yaml

apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mysql
spec:
  serviceName: "mysql"
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - name: mysql
        image: mysql:5.7
        ports:
        - containerPort: 3306
          name: mysql
        volumeMounts:
        - name: mysql-storage
          mountPath: /var/lib/mysql
  volumeClaimTemplates:
  - metadata:
      name: mysql-storage
    spec:
      accessModes: [ "ReadWriteOnce" ]
      resources:
        requests:
          storage: 1Gi
```

StatefulSet Lifecycle
- Creation: Pods are created sequentially, each with a unique identity.
- Update: Pods are updated one at a time in a controlled order.
- Deletion: When scaled down, pods are terminated in reverse order.

## StatefulSet vs Deployment

| Feature           | StatefulSet                                             | Deployment                          |
|-------------------|---------------------------------------------------------|-------------------------------------|
| **Pod Identity**  | Unique and stable across rescheduling                   | Random                              |
| **Storage**       | Persistent volumes for each pod                         | Shared storage or ephemeral         |
| **Pod Management**| Ordered (creation, scaling, updating, deletion)         | Random                              |
| **Use Case**      | Databases, stateful applications                        | Stateless applications, web servers |
