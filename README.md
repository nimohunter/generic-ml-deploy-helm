# Helm chart explian(generic)
Here is use helm chart to control the whole ml project to depoly in kubernetes. here is helm chart code repo: [generic-ml-deploy-helm](https://github.com/nimohunter/generic-ml-deploy-helm)
you can see we have three env:

* `values-dev.yaml` for Development
* `values-staging.yaml` for Staging
* `values-prod.yaml` for Production

```bash
# local usage Deploy using a specific Docker image with namespace in staging
helm install my-ml-release ./ -f values-dev.yaml  --namespace dev  --set image.repository=duluku/flask-hello-world
```

### Seperate depoly location (Isolation)

we may deploy the different env in different kubernetes, seperate the data and traffic.

but it's cost a lot, so sometimes we use namespace to seperate, deply the application into these namespaces using Helm and specifying the namespace during the deployment.

Create all the namespace in the minikube
```bash
minikube start

kubectl create namespace dev
kubectl create namespace staging
kubectl create namespace prod
```

deploy :

```bash
 helm install my-ml-release ./ -f values-dev.yaml  --namespace dev  --set image.repository=duluku/flask-hello-world
 helm install my-ml-release ./ -f values-staging.yaml  --namespace staging  --set image.repository=duluku/flask-hello-world
 helm install my-ml-release ./ -f values-prod.yaml  --namespace prod  --set image.repository=duluku/flask-hello-world
```


### Case Test 
run the test, and we can see the success, and the dev pod return the dev info "Hello, World From Dev Env" 
```bash
helm test my-ml-release --namespace dev
helm test my-ml-release --namespace staging
# we don't think we need test in prod environment.
# helm test my-ml-release --namespace prod

# check the log
kubectl logs -n dev -l "job-name=my-ml-release-test-connection"
```

or we can use proxy to check the flask response, see the different response:

```bash 
kubectl proxy

curl http://localhost:8001/api/v1/namespaces/dev/services/my-ml-release-generic-ml-deploy-helm:5000/proxy/
Hello, World From Dev Env%  
curl http://localhost:8001/api/v1/namespaces/staging/services/my-ml-release-generic-ml-deploy-helm:5000/proxy/
Hello, World From Staging Env%                                                 
curl http://localhost:8001/api/v1/namespaces/prod/services/my-ml-release-generic-ml-deploy-helm:5000/proxy/
Hello, World From Prod Env%    

```

### Healthy detect And auto scaling (availability)
Autoscaling allows the application to handle changes in load by automatically adjusting the number of running instances.Which can reduces costs and maintains application performance. 

Health checks (liveness and readiness probes) ensure that the application is running smoothly and can serve traffic. Liveness probes keep the application running by restarting containers that fail, and readiness probes determine when a container is ready to start accepting traffic.

`values-prod.yaml` enable the function.

```yaml
enableAutoscaling: true
autoscaling:
  minReplicas: 2
  maxReplicas: 10
  targetCPUUtilizationPercentage: 50
```