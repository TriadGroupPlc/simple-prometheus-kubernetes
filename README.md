# Simple Prometheus on Kubernetes
A generic set of YAML files for deploying Prometheus to a Kubernetes cluster

Kubernetes exposes metrics that Prometheus can scrape, and it also allows you to use its API to discover other services that have available metrics endpoints.


### Contents
The manifests directory contains a number of YAML files that will create a _monitoring_ namespace and deploy the required resources for Prometheus.

* A namespace (monitoring)
* A Service account for Prometheus to use
* A cluster role and binding that allows that user to access the required Kubernetes APIs
* A config map with the required configuration file for Prometheus (prometheus.yml). To configure what Prometheus collects and how often edit this.
* A deployment that runs Prometheus and exposes it through a LoadBalancer service
* Optionally - A test endpoint that puts out some data that can be scraped

Note: it doesn't use any persistant storage so if you restart it you'll lose the metrics collected so far. To change this, update  _manifests/prometheus/04-deployment.yml_

### Setup
To deploy simply run apply in the manifests/prometheus directory:
```
kubectl apply -f manifests/prometheus
```

Once it's started (or before) you can also deploy the test endpoint:
```
kubectl apply -f manifests/test-endpoint.yml
```

#### Web UI
You can then access the Prometheus UI at the endpoint provided by the service on port 8080
```
kubectl get svc
```

http://\<IP Address>:8080