# Linode Kubernetes GitOps

## Objective

This document will serve as a guide to set up flux and helm controllers for new kubernetes clusters.

## Steps

1. Setup PAT token

```
export GITHUB_TOKEN=<gh-token>
```

2. bootstrap helm controller in kubernetes

```
flux bootstrap github \
  --token-auth \
  --owner=<my-github-username> \
  --repository=my-repository-name \
  --branch=main \
  --path=clusters/id-cluster \
  --personal
```

## Key Infrastructure Components

### Fluentd
[fluent-plugin-elasticsearch](https://github.com/uken/fluent-plugin-elasticsearch?tab=readme-ov-file#suppress_type_name)

### Alert and Monitoring - Grafana & Prometheus

### Custom docker registry

## Additional Link

## Access Kibana and Grafana
Run the following command to obtain the credentials
```
kubectl get secret quickstart-es-elastic-user -n elastic -o go-template='{{.data.elastic | base64decode}}'
kubectl get secret prometheus-operator-grafana -n monitoring -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

## Redis Insights
As redis insights currently does not support authentication, we will use ingress gateway basic auth to restrict access to the service.

1. Create basic auth credentials
```
htpasswd -c auth anvesh
```
2. Save as secret in redis namespace
```
kubectl create secret generic redis-insights-auth --from-file=auth -n redis
kubectl create secret generic akhq-auth --from-file=auth -n kafka
```
3. Ingress gateway will use this secret to authenticate requests to the service

[Repo structure guide](https://github.com/fluxcd/flux2-kustomize-helm-example)

4. Add redis grafana dashboard
```
Redis Data Source
https://redisgrafana.github.io/redis-datasource/overview/

Redis Dashboard template
https://grafana.com/grafana/dashboards/12776-redis/
```