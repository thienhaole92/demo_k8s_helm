# [Helm](https://helm.sh)

## Install Helm CLI
```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```
## Show the version for Helm
```
helm version
```

## Add a chart repository
```	
https://charts.helm.sh/stable
```
## Search for stable release versions matching the keyword "nginx"
```
helm search repo nginx
```
## Install charts from the Helm Hub
```
k8s helm install nginx bitnami/nginx --namespace demo --create-namespace --wait
```
## Uninstall a release
```
helm uninstall nginx --namespace demo
```
## Create a new chart with the given name
```
helm create echoserver
```
## Debugging Templates
```
helm install echoserver --dry-run --debug ./echoserver --set service.type=LoadBalancer
```
## Install a chart
```
helm install echoserver ./echoserver --set service.type=LoadBalancer
```
## Uninstall a chart
```
helm uninstall echoserver
```
## Upgrade a release
```
helm upgrade echoserver ./echoserver --set service.type=LoadBalancer
```
## Fetch release history
