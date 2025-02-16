This repo follows Debezium official documentation [Deploying Debezium on Kubernetes](https://debezium.io/documentation/reference/stable/operations/kubernetes.html), but modified for Azure Kubernetes Service and Azure Container Registry.

Please view this [blog post](https://anhcodes.dev/blog/deploy-debezium-aks/) for more details on how to use this repo

Deploy Strimzi using Helm:
```bash
# add Helm chart repo for Strimzi
helm repo add strimzi https://strimzi.io/charts/
helm repo update

# create kafka namespace
kubectl create ns debezium-example

# install Strimzi (strimzi-kafka is the release name)
helm install strimzi-kafka strimzi/strimzi-kafka-operator -n debezium-example --set createGlobalResources=false