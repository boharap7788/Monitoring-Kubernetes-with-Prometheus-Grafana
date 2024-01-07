# Monitoring-Kubernetes-with-Prometheus-Grafana
   Prometheus Grafana Monitoring on Kubernetes using Helm

# To install Helm using Snap, run the following command:
  sudo snap install helm --classic

# Once the installation is complete, you should be able to use the Helm command to add the Prometheus Community Helm repository. After installing Helm, you can re-run the following command:
  helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

# Search repo of prometheus
  helm search repo prometheus

# Update repo 
  helm repo update

# install Prometheus without creating our own template and only use default values:
  helm install prometheus prometheus-community/prometheus
# To check all the details repalted to prometheus helm packages and kubernetes OBjects
  kubectl get pods 

# To expose prometheus to outside accesible
kubectl expose service prometheus-server --type=NodePort --target-port=9090 --name=prometheus-service-ext

# Check The service are there or not 
  kubeclt get service
  
# Check service URL to access outside 
  minikube service service-name

# To add the Grafana Helm chart repository, you can use the following command:
  helm repo add grafana https://grafana.github.io/helm-charts

# To install Grafana using the official Grafana Helm chart, you can use the following command
  helm install grafana grafana/grafana
  helm list
# To expose grafana to outside accesible
kubectl expose service grafana --type=NodePort --target-port=3000 --name=grafana-service-ext

# To get password for grafana , Type below command 
 kubectl get secret --namespace default grafana -o yaml
==> Below admin-password & admin-user is encrypted so we need to decrypt it to login to grafana
data:
  admin-password: ZDVmcGphUXg4eFN4alBkbmhKOHNuRTVSVFNQWnhNS0IyRUk4cU9XVw==
  admin-user: YWRtaW4=
 
# Command to decrypt it 
  echo "put(admin-password/admin-user)" | openssl base64 -d ; echo
  
  
# Login to grafana the create dashboard by importing id 6417 ,3662 , you will get dashboard from grafana Labs 
https://grafana.com/grafana/dashboards/6417-kubernetes-cluster-prometheus/

https://grafana.com/grafana/dashboards/3662-prometheus-2-0-overview/

# To stop or uninstall all running resources deployed through Helm, you can use the following command:

helm ls --all --short | xargs -L1 helm uninstall



