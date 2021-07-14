# How to 

*Install kind(microk8s, k3s, cloud sollution).*

```sh
	curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.11.1/kind-linux-amd64
	chmod +x ./kind
	mv ./kind /some-dir-in-your-PATH/kind
```

*Install helm3.*

```sh
	curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
```

*helm add repo bitnami*

```sh
	helm repo add bitnami https://charts.bitnami.com/bitnami
```

repo of charts [bitnami](https://github.com/bitnami/charts/tree/master/bitnami)

# Usage

## 1. Prometheus Operator

Create prometheus-operator/values.yaml file for configuration.

```sh
helm install operator bitnami/kube-prometheus -f prometheus-operator/values.yaml

kubectl port-forward alertmanager-operator-kube-prometheus-alertmanager-0 9093:9093

kubectl port-forward prometheus-operator-kube-prometheus-prometheus-0 9090:9090
```

## 2. Jenkins

Create jenkins/values.yaml file for configuration.

```sh
helm install jenkins bitnami/jenkins -f jenkins/values.yaml

metadata=$(kubectl get pods -l app.kubernetes.io/instance=jenkins -o jsonpath="{.items[0].metadata.name}")

kubectl port-forward $metadata 8080:8080
```

## 3. Our Helm

Create application chart.

```sh
helm create application

helm package .

helm install application application-0.1.0.tgz

metadata=$(kubectl get pods -l app.kubernetes.io/name=application -o jsonpath="{.items[0].metadata.name}")

kubectl port-forward $metadata 8080:80

```

## 4. Questions
    / / / 
   (0 . 0)
    \ º /

