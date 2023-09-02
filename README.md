# mysql-grafana  


# 1. Install mysql database on cluster:  

    helm repo add bitnami https://charts.bitnami.com/bitnami
    helm upgrade --install mysql bitnami/mysql 
    kubectl get pods 
    kubectl exec -it mysql-0 -- /bin/bash


# 2. Install Kube-Prometheus-Stack on cluster:  

Reference Documentation is as below:  

https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack

This will installs the kube-prometheus stack, a collection of Kubernetes manifests, Grafana dashboards, and Prometheus rules combined with documentation and scripts to provide easy to operate end-to-end Kubernetes cluster monitoring with Prometheus using the Prometheus Operator.

Below Steps needs to be followed:

    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    helm repo update
    kubectl create ns metrics
    kubectl config set-context --current --namespace=metrics

    helm upgrade --install grafana prometheus-community/kube-prometheus-stack

# 3. Install Prometheus Mysql Exporter  

    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    helm repo update

    helm upgrade --install mysql-exporter prometheus-community/prometheus-mysql-exporter -f mysql-exporter-values.yaml

# 4. Install Prometheus Mysql Exporter Dashboard  

    https://grafana.com/grafana/dashboards/14057-mysql/
    https://grafana.com/grafana/dashboards/7362-mysql-overview/

    Add the below ids as Grafana Dashboards and monitor mysql db 
    
        14057
        7362