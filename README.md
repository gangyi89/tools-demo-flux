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
  --path=clusters/sg-cluster \
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

[Repo structure guide](https://github.com/fluxcd/flux2-kustomize-helm-example)