# Actual operation

git clone this helm chart, and we can run the the following command

```bash
nimodai@NIMODAI-MB1 OtherProjects % cd generic-ml-deploy-helm
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % minikube start
😄  minikube v1.33.1 on Darwin 14.5 (arm64)
✨  Automatically selected the docker driver
📌  Using Docker Desktop driver with root privileges
👍  Starting "minikube" primary control-plane node in "minikube" cluster
🚜  Pulling base image v0.0.44 ...
🔥  Creating docker container (CPUs=2, Memory=7792MB) ...
🐳  Preparing Kubernetes v1.30.0 on Docker 26.1.1 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔗  Configuring bridge CNI (Container Networking Interface) ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: storage-provisioner, default-storageclass
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl create namespace dev
namespace/dev created
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % helm install my-ml-release ./ -f values-dev.yaml  --namespace dev  --set image.repository=duluku/flask-hello-world
NAME: my-ml-release
LAST DEPLOYED: Wed Jun 26 10:22:31 2024
NAMESPACE: dev
STATUS: deployed
REVISION: 1
NOTES:
1. Get the application URL by running these commands:
  export POD_NAME=$(kubectl get pods --namespace dev -l "app.kubernetes.io/name=generic-ml-deploy-helm,app.kubernetes.io/instance=my-ml-release" -o jsonpath="{.items[0].metadata.name}")
  export CONTAINER_PORT=$(kubectl get pod --namespace dev $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")
  echo "Visit http://127.0.0.1:8080 to use your application"
  kubectl --namespace dev port-forward $POD_NAME 8080:$CONTAINER_PORT
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl get pods -n dev
NAME                                                    READY   STATUS              RESTARTS   AGE
my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8   0/1     ContainerCreating   0          7s
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl get pods -n dev
NAME                                                    READY   STATUS              RESTARTS   AGE
my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8   0/1     ContainerCreating   0          9s
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl get pods -n dev
NAME                                                    READY   STATUS              RESTARTS   AGE
my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8   0/1     ContainerCreating   0          14s
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl get pods -n dev
NAME                                                    READY   STATUS              RESTARTS   AGE
my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8   0/1     ContainerCreating   0          16s
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl get pods -n dev
NAME                                                    READY   STATUS              RESTARTS   AGE
my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8   0/1     ContainerCreating   0          17s
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl get pods -n dev
NAME                                                    READY   STATUS              RESTARTS   AGE
my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8   0/1     ContainerCreating   0          18s
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl get pods -n dev
NAME                                                    READY   STATUS              RESTARTS   AGE
my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8   0/1     ContainerCreating   0          19s
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl get pods -n dev
NAME                                                    READY   STATUS              RESTARTS   AGE
my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8   0/1     ContainerCreating   0          20s
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl get pods -n dev
NAME                                                    READY   STATUS              RESTARTS   AGE
my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8   0/1     ContainerCreating   0          21s
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl get pods -n dev
NAME                                                    READY   STATUS              RESTARTS   AGE
my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8   0/1     ContainerCreating   0          22s
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl get pods -n dev
NAME                                                    READY   STATUS              RESTARTS   AGE
my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8   0/1     ContainerCreating   0          32s
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl get pods -n dev
NAME                                                    READY   STATUS              RESTARTS   AGE
my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8   0/1     ContainerCreating   0          33s
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl get pods -n dev
NAME                                                    READY   STATUS              RESTARTS   AGE
my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8   0/1     ContainerCreating   0          34s
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl describe pod my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8 -n dev
Name:             my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8
Namespace:        dev
Priority:         0
Service Account:  default
Node:             minikube/192.168.49.2
Start Time:       Wed, 26 Jun 2024 10:22:31 +0800
Labels:           app.kubernetes.io/instance=my-ml-release
                  app.kubernetes.io/managed-by=Helm
                  app.kubernetes.io/name=generic-ml-deploy-helm
                  app.kubernetes.io/version=1.16.0
                  helm.sh/chart=generic-ml-deploy-helm-0.1.0
                  pod-template-hash=79d9dcf88d
Annotations:      <none>
Status:           Pending
IP:               
IPs:              <none>
Controlled By:    ReplicaSet/my-ml-release-generic-ml-deploy-helm-79d9dcf88d
Containers:
  generic-ml-deploy-helm:
    Container ID:   
    Image:          duluku/flask-hello-world:dev
    Image ID:       
    Port:           5000/TCP
    Host Port:      0/TCP
    State:          Waiting
      Reason:       ContainerCreating
    Ready:          False
    Restart Count:  0
    Limits:
      cpu:     100m
      memory:  128Mi
    Requests:
      cpu:        100m
      memory:     128Mi
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-b9nbq (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   False 
  Initialized                 True 
  Ready                       False 
  ContainersReady             False 
  PodScheduled                True 
Volumes:
  kube-api-access-b9nbq:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   Guaranteed
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  61s   default-scheduler  Successfully assigned dev/my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8 to minikube
  Normal  Pulling    61s   kubelet            Pulling image "duluku/flask-hello-world:dev"
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl describe pod my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8 -n dev
Name:             my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8
Namespace:        dev
Priority:         0
Service Account:  default
Node:             minikube/192.168.49.2
Start Time:       Wed, 26 Jun 2024 10:22:31 +0800
Labels:           app.kubernetes.io/instance=my-ml-release
                  app.kubernetes.io/managed-by=Helm
                  app.kubernetes.io/name=generic-ml-deploy-helm
                  app.kubernetes.io/version=1.16.0
                  helm.sh/chart=generic-ml-deploy-helm-0.1.0
                  pod-template-hash=79d9dcf88d
Annotations:      <none>
Status:           Pending
IP:               
IPs:              <none>
Controlled By:    ReplicaSet/my-ml-release-generic-ml-deploy-helm-79d9dcf88d
Containers:
  generic-ml-deploy-helm:
    Container ID:   
    Image:          duluku/flask-hello-world:dev
    Image ID:       
    Port:           5000/TCP
    Host Port:      0/TCP
    State:          Waiting
      Reason:       ContainerCreating
    Ready:          False
    Restart Count:  0
    Limits:
      cpu:     100m
      memory:  128Mi
    Requests:
      cpu:        100m
      memory:     128Mi
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-b9nbq (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   False 
  Initialized                 True 
  Ready                       False 
  ContainersReady             False 
  PodScheduled                True 
Volumes:
  kube-api-access-b9nbq:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   Guaranteed
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  66s   default-scheduler  Successfully assigned dev/my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8 to minikube
  Normal  Pulling    66s   kubelet            Pulling image "duluku/flask-hello-world:dev"
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl log  my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8 -n dev
error: unknown command "log" for "kubectl"

Did you mean this?
	top
	logs
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl logs  my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8 -n dev
 * Serving Flask app 'app'
 * Debug mode: off
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:5000
 * Running on http://10.244.0.3:5000
Press CTRL+C to quit
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl get pods -n dev
NAME                                                    READY   STATUS    RESTARTS   AGE
my-ml-release-generic-ml-deploy-helm-79d9dcf88d-s4pq8   1/1     Running   0          96s
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % helm test my-ml-release --namespace dev
NAME: my-ml-release
LAST DEPLOYED: Wed Jun 26 10:22:31 2024
NAMESPACE: dev
STATUS: deployed
REVISION: 1
TEST SUITE:     my-ml-release-test-connection
Last Started:   Wed Jun 26 10:24:12 2024
Last Completed: Wed Jun 26 10:24:25 2024
Phase:          Succeeded
TEST SUITE:     my-ml-release-test-response
Last Started:   Wed Jun 26 10:24:25 2024
Last Completed: Wed Jun 26 10:24:37 2024
Phase:          Succeeded
NOTES:
1. Get the application URL by running these commands:
  export POD_NAME=$(kubectl get pods --namespace dev -l "app.kubernetes.io/name=generic-ml-deploy-helm,app.kubernetes.io/instance=my-ml-release" -o jsonpath="{.items[0].metadata.name}")
  export CONTAINER_PORT=$(kubectl get pod --namespace dev $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")
  echo "Visit http://127.0.0.1:8080 to use your application"
  kubectl --namespace dev port-forward $POD_NAME 8080:$CONTAINER_PORT
nimodai@NIMODAI-MB1 generic-ml-deploy-helm % kubectl proxy
Starting to serve on 127.0.0.1:8001


```