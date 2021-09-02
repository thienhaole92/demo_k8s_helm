# Autoscaling in EKS (on aws managed k8s)
## Deploy the application using helm:
```
helm upgrade --install nodejs-test ./autoscaling --namespace autoscaling --create-namespace --wait
```
## Destroy the application
```
helm uninstall nodejs-test ./autoscaling --namespace autoscaling
```

## Test the application deployment:
- Check if application has working loadbalancer `hostname` or `ip` -> `curl <HOSTNAME|IP>:<PORT>`
- Open new window in terminal and watch HPA -> `kubectl get hpa -n release -w`
- Open 2/3 terminal window and execute `while true; do curl -s < <HOSTNAME|IP>:<PORT>; done` in both of them to increase the load on service
- In few seconds you will notice that replicas has increased for the nodejs-test deployment because of HPA

## Result/Output
Test results are as follows:

Before load test:
```
(djo) ➜  autoscaling kubectl get hpa -n autoscaling -w   
NAME                      REFERENCE                            TARGETS            MINPODS   MAXPODS   REPLICAS   AGE
nodejs-test-autoscaling   Deployment/nodejs-test-autoscaling   57%/60%, 10%/50%   1         10        10         117s
```
During load test:

```bash
(djo) ➜  autoscaling kubectl get hpa -n autoscaling -w
NAME                      REFERENCE                            TARGETS            MINPODS   MAXPODS   REPLICAS   AGE
nodejs-test-autoscaling   Deployment/nodejs-test-autoscaling   57%/60%, 10%/50%   1         10        10         2m59s
nodejs-test-autoscaling   Deployment/nodejs-test-autoscaling   57%/60%, 16%/50%   1         10        10         3m5s
nodejs-test-autoscaling   Deployment/nodejs-test-autoscaling   56%/60%, 15%/50%   1         10        10         3m20s
nodejs-test-autoscaling   Deployment/nodejs-test-autoscaling   56%/60%, 10%/50%   1         10        10         3m36s
nodejs-test-autoscaling   Deployment/nodejs-test-autoscaling   56%/60%, 11%/50%   1         10        10         3m51s
nodejs-test-autoscaling   Deployment/nodejs-test-autoscaling   57%/60%, 14%/50%   1         10        10         4m6s
nodejs-test-autoscaling   Deployment/nodejs-test-autoscaling   56%/60%, 20%/50%   1         10        10         4m21s

```

After load test:

```bash
(djo) ➜  autoscaling kubectl get hpa -n autoscaling   
NAME                      REFERENCE                            TARGETS            MINPODS   MAXPODS   REPLICAS   AGE
nodejs-test-autoscaling   Deployment/nodejs-test-autoscaling   55%/60%, 31%/50%   1         10        10         5m12s
```
