# kubernetes-basic-scripts
kubernetes fundamentals


Create Pod

Commands

1. Create pod

`kubectl run mynginx —image nginx`

1. Create By file

`kubectl create -f pods/pod-definition.yml`

1. Update By File

`kubectl apply -f pods/pod-definition.yml`

1. Extract the configs to file

`kubectl get pod <pod-name> -o yaml > pod-definition.yaml`


View the configs

kubectl describe pod <podId>


ReplicaSet

apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-nginx-replica-app
  labels:
    app: myapp
    type: BE
spec:
  template:
      metadata:
        name: my-prod
        labels:
          app: sample
      spec:
        containers:
          - name: my-nginx-container
            image: nginx
  replicas: 3
  selector: 
    matchLabels:
      app: sample


Update configs

kubectl replace -f replica-set/rc-definition-v2.yml

Scale Configs

kubectl scale --replicas=5 -f replica-set/rc-definition-v2.yml

kubectl scale --replicas=5 rs new-replica-set



Deployments


apiVersion: apps/v1
kind: Deployment
metadata:
  name: hstudio-prod
spec:
  replicas: 2
  template:
    metadata:
      labels:
        type: BE
    spec:
      containers:
      - name: nginx-controller
        image: nginx
  selector:
    matchLabels:
      type: BE


kubectl get deploy

