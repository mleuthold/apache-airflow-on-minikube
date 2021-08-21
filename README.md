# Apache Airflow on Minikube
Run Apache Airflow on Minikube with DAG sync from S3 bucket

# Prerequisite
Development environment is considered a MacBook Pro.

- helm v3
```shell
brew install helm
```
- minikube
```shell
brew install minikube

brew unlink minikube
brew link minikube
```

# Configure Minikube
Minikube runs with 2 CPUs and 2 GB Memory by default. This results in time out when installing Apache Airflow. \
Therefore increase the resources available to Minikube.
```shell
minikube config set cpus 4
minikube config set memory 8192
```

# Install Apache Airflow on Minikube
```shell
minikube start

kubectl create namespace airflow
helm repo add apache-airflow https://airflow.apache.org
helm install airflow apache-airflow/airflow --namespace airflow

minikube stop
```

# Update Apache Airflow on Minikube
```shell
kubectl config set-context --current --namespace=airflow
helm upgrade --install airflow apache-airflow/airflow \
  -f values.yaml
```