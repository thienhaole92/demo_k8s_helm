# [Kubernetes](https://kubernetes.io/)
## Create namespace
```
kubectl apply -f echoserver-namespace.yaml
```
## Create deployment
```
kubectl apply -f echoserver-deployment.yaml
```
## Create service
```
kubectl apply -f echoserver-service.yaml
```
## This is what ends up running after your installation
```
pod/echoserver-864697899f-j4zwk   1/1     Running   0          13s

NAME                 TYPE           CLUSTER-IP       EXTERNAL-IP                                                                    PORT(S)        AGE
service/echoserver   LoadBalancer   10.100.193.204   a27839400ef074be1b3fdc0166d5962c-2059871604.ap-southeast-1.elb.amazonaws.com   80:31653/TCP   27s

NAME                         READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/echoserver   1/1     1            1           14s

NAME                                    DESIRED   CURRENT   READY   AGE
replicaset.apps/echoserver-864697899f   1         1         1       14s

```
