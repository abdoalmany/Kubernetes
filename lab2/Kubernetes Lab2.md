# Kubernetes Lab2

**1- Deploy a pod named nginx-pod using the nginx:alpine image with the labels set to   tier=backend.**

`$ kubectl create -f nginxPod.yaml`

**2- Deploy a test pod using the nginx:alpine image.**

`$ kubectl create deploy nginx-test-pod --image=nginx:alpine`

`deployment.apps/nginx-test-pod created`

**3- Create a service backend-service to expose the backend application within the cluster on port 80.**

`$ kubectl apply -f ./nginx-service.yaml`

`service/nginx-pod created`

**4- try to curl the backend-service from the test pod. What is the response?**

`curl 172.17.0.22:80
curl: (7) Failed to connect to 172.17.0.22 port 80: No route to host`

**5- Create a deployment named web-app using the image nginx with 2 replicas**

`$ kubectl apply -f web-app.yaml 
deployment.apps/web-app created`

**6- Expose the web-app as service web-app-service application on port 80 and nodeport 30082 on the nodes on the cluster**

`kubectl apply -f web-app-service.yaml 
service/web-app created`

**7- access the web app from the node**

`curl 10.101.136.111
curl: (28) Failed to connect to 10.101.136.111 port 80: Connection timed out`

**8- How many Nodes exist on the system?**

`$ kubectl get nodes
NAME       STATUS   ROLES                  AGE   VERSION
minikube   Ready    control-plane,master   20d   v1.23.3`

**9- Do you see any taints on master ?**

NO

**10- Apply a label color=blue to the master node**

`$ kubectl label node minikube color=blue
node/minikube labeled`

**11- Create a new deployment named blue with the nginx image and 3 replicas**

​     **Set Node Affinity to the deployment to place the pods on master only**
​     **NodeAffinity: requiredDuringSchedulingIgnoredDuringExecution**
​     **Key: color**
​     **values: blue**
**12- How many DaemonSets are created in the cluster in all namespaces?**
**13- what DaemonSets exist on the kube-system namespace?**
**14- What is the image used by the POD deployed by the kube-proxy DaemonSet**
**15- Deploy a DaemonSet for FluentD Logging. Use the given specifications.**
​      **Name: elasticsearch**
​      **Namespace: kube-system**
​      **Image: k8s.gcr.io/fluentd-elasticsearch:1.20**
**16- Create a taint on node01 with key of spray, value of mortein and effect of NoSchedule**
**17- Create a new pod named mosquito with the NGINX image**
**18- What is the state of the mosquito POD?**
**19- Create another pod named bee with the NGINX image, which has a toleration set to the taint Mortein**
​        **Image name: nginx**
​    **• Key: spray**
​    **• Value: mortein**
​    **• Effect: NoSchedule**
​    **• Status: Running**
**20- Remove the taint on master/controlplane, which currently has the taint effect of NoSchedule**
**21- What is the state of the pod mosquito now and Which node is the POD mosquito on?**

**22- Create a job countdown-job.**
**The container should be named as container-countdown-job**
**Use image debian:latest, and restart policy should be Never.**
**Use command for i in ten nine eight seven six five four three two one ; do echo $i ; done**