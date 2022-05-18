# k8s_monitor_prom_grafana
#### Prometheus and Grafana Monitoring on Kubernetes
#### First we must create ns and use helm to deploy
```
kubectl create ns kube-monitor

helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update

helm install  --namespace kube-monitor kube-prometheus bitnami/kube-prometheus --set global.imageRegistry=artifactory.spng.ir/docker

helm install  --namespace kube-monitor kube-grafana bitnami/grafana --set global.imageRegistry=artifactory.spng.ir/docker
```
#### to check ns pods
```
kubectl -n kube-monitor get pods -o wide
```
####  ingress for grafana
```
kubectl apply -f grafana-ingress.yml
```
#### URL: https://grafana.example.com/login 

#### grafana admin password:
```
echo "$(kubectl  get secret kube-grafana-admin --namespace kube-monitor -o jsonpath="{.data.GF_SECURITY_ADMIN_PASSWORD}" | base64 --decode)"
```
#### ingress for Prometheus
```
kubectl apply -f grafana-ingress.yml
```
#### URL: https://prom.example.com
#### prometheus datastore:
#### http://kube-prometheus-prometheus.kube-monitor:9090

#### Grafana Useful Dashboard for k8s:
##### https://grafana.com/grafana/dashboards/10000 
##### https://grafana.com/grafana/dashboards/315
##### https://grafana.com/grafana/dashboards/13838
##### https://grafana.com/grafana/dashboards/11663
##### https://grafana.com/grafana/dashboards/6417 
