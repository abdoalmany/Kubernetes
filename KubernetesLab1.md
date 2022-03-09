# Kubernetes Lab 1 



**1- Install k8s cluster (minikube) (optional you can use https://www.katacoda.com/courses/kubernetes/playground)**

![](https://imgur.com/3VOPJQ2.png)

**2- Create a pod with the name Redis and with the image Redis.**

```bash
kubectl create deployment redis --image=redis
```

![](https://imgur.com/enzNe1Y.png)

**3- Create a pod with the name Nginx and with the image nginx123.**

 **Use a pod-definition YAML file. And yes the image name is wrong!**

```bash
kubectl create deployment nginx --image=nginx123
```

![](https://imgur.com/F4b80p6.png)

**4- What is the Nginx pod status?**

```bash
kubectl get pods
```

![](https://imgur.com/8wwrLR0.png)

**5- Change the Nginx pod image to Nginx check the status again**

```bash
kubectl edit deploy nginx
kubectl get deploy
```

![](https://imgur.com/oFAuff1.png)

**6- How many ReplicaSets exist on the system?**

```bash
kubectl get rs
```

![](https://imgur.com/fa74cjf.png)

**7- Create a ReplicaSet with**

  **name= replica-set-1**

  **image= busybox**

  **replicas= 3**

```bash
kubectl create deploy replica-set-1 --image=busybox --replicas=3
```

![](https://imgur.com/45cdOBe.png)

**8- Scale the ReplicaSet replica-set-1 to 5 PODs.**

![](https://imgur.com/QQiU9Mm.png)

**9- How many PODs are READY in the replica-set-1?**

> 0

**10- Delete any one of the 5 PODs then check How many PODs exist now?**

  **Why are there still 5 PODs, even after you deleted one?**

```
kubectl delete pod replica-set-1-7bdc749c8c-9mnpc
```

![](https://imgur.com/gqhKxXY.png)

> Because of that replica set created a new pod to keep them 5 in the replica set .

**11- How many Deployments and ReplicaSets exist on the system?**

​	3 Deployments 

​	4 Replica sets 

![](https://imgur.com/WTq1piP.png)

**12- Create a Deployment with**

  **name= deployment-1**

  **image= busybox**

  **replicas= 3**

```bash
kubectl create deploy deployment-1 --image=busybox  --replicas=3
```

**13- How many Deployments and ReplicaSets exist on the system now?**

> 4 Deployments

> 5 Replicasets

**14- How many pods are ready with the deployment-1?**

> 0

**15- Update deployment-1 image to Nginx then check the ready pods again**

> 3

**16- Run kubectl describe deployment deployment-1 and check events** 

  **What is the deployment strategy used to upgrade the deployment-1?** 

> StrategyType:           RollingUpdate

**17- Rollback the deployment-1** 

```bash
kubectl rollout undo deployment deployment-1
```

  **What is the used image with the deployment-1?**

> Image:        busybox

**18- How many Namespaces exist on the system?**

```bash
kubectl get namespace
```

> NAME                   			STATUS   AGE
> default                				Active   28h
> kube-node-lease      		 Active   28h
> kube-public            			Active   28h
> kube-system              		Active   28h
> kubernetes-dashboard    Active   28h

> 5 name spaces

**19- How many pods exist in the kube-system namespace?**

```bash
kubectl get pods --namespace=kube-system
```

> 7 pods

**20- Create a deployment with**

   **Name: beta**

   **Image: Redis**

   **Replicas: 2**

   **Namespace: finance**

   **Resources Requests:**

​    **CPU: .5 vcpu**

​    **Mem: 1G**

  **Resources Limits:**

   **CPU: 1 vcpu**

   **Mem: 2G**

```bash
kubectl create -f my-namespace.yml
```

```bash
kubectl create -f ./beta.yaml
```

```bash
kubectl get deployment beta
```

> NAME   READY   UP-TO-DATE   AVAILABLE   AGE
>
> beta  	  2/2   				  	  2            2           37m
