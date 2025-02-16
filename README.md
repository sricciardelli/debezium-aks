This repo follows Debezium official documentation [Deploying Debezium on Kubernetes](https://debezium.io/documentation/reference/stable/operations/kubernetes.html), but modified for Azure Kubernetes Service and Azure Container Registry.

Please view this [blog post](https://anhcodes.dev/blog/deploy-debezium-aks/) for more details on how to use this repo

Deploy kafka cluster
1. Create debezium-cluster kafka cluster with kafka.yml
```bash
kubectl create -n kafka -f kafka.yml
# Wait until kafka cluster ready 
kubectl wait kafka/debezium-cluster --for=condition=Ready --timeout=300s -n kafka
```

1. Validate kafka cluster has been created
```bash
kubectl get kafka -n kafka
kubectl get service -n kafka
kubectl get deployment -n kafka
kubectl get pod -n kafka
```

1. Deploy kafka-connect resource
```bash
kubectl create -n kafka -f kafka-connect-build.yml
```

1. Validate the kafka connect cluster
```bash
kubectl get kafkaconnect -n kafka
kubectl get service -n kafka
kubectl run kafka-topics -ti --image=quay.io/strimzi/kafka:latest-kafka-3.9.0 --rm=true --restart=Never -- bin/kafka-topics.sh --bootstrap-server debezium-cluster-kafka-bootstrap.kafka.svc:9092 --list
```