To access the Prometheus Node Exporter, run the following command:

```bash
kubectl port-forward service/prometheus-prometheus-node-exporter 9100 --namespace=prometheus

kubectl port-forward deployment/prometheus-grafana 3000 --namespace=prometheus # To access Grafana

kubectl port-forward service/alertmanager-operated 9093 --namespace=prometheus # To access Alert-Manager

localhost:<port> # Access all svcs over the web

```
To check the status of the pods, run:

```bash
kubectl get pods -n prometheus
```

- Everything runs as a pod in the prometheus namespace and can be accessed by port forwarding. If in AWS, services can be accessed using the Load Balancer IP by exposing services.

- Node Exporter: Scrapes hardware, i.e., infrastructure metrics, and exposes the /metrics endpoint to the Prometheus server, which pulls and stores the data in the TSDB.

Access metrics:

```bash
kubectl get svc -n prometheus

minikube ssh

curl <node-exporter IP>:<exposed-port>/metrics
```

PromQL
Total Number of Pod Restarts

To query the total number of pod restarts, use the following PromQL:

```bash
kube_pod_container_status_restarts_total
```
![PromQL](https://raw.githubusercontent.com/RanjanPRS/Monitoring-and-Logging/main/PROMETHEUS/kube_pod_container_status_restarts_total.png)

Create a Pod That Always Crashes

You can create a pod that always crashes with the following command:

```bash
kubectl run busybox-crash --image=busybox -- /bin/sh -c "exit 1"
```

Now check the UI to view the number of restarts.

