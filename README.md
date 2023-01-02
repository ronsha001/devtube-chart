
# Welcome to DevTube Helm Chart

## Dependencies
- MongoDB

## Description
DevTube chart will be used for applying the DevTube Web Application on your Kubernetes cluster.
This chart will create the following services:
- DevTube Frontend (React.js application)
- DevTube API (Express.js API)
- MongoDB

For editing the chart values you can find `values.yaml` in `devtube` directory.
There are 2 possible ways to apply this chart to your Kubernetes cluster, executing the `helm install <Release-Name> devtube/` command in root directory, this will apply the helm chart directly on your kubernetes cluster without any platform that can manage it, or you can execute the command `kubectl apply -f application.yaml` also in root directory, this will tell your ArgoCD to apply and manage all chart services such as Deployments, Statefulsets and more..

## Values
You can read the default list of values that this chart provides.
- `namespace: devtube`
- `ingress:`
  - `enabled: true`
  - `certificate:`
    - `enabled: true`
    - `email: ronsh0111@gmail.com`
    - `host: devtube.ddns.net`
- `mongodb:`
  - `architecture: replicaset`
  - `useStatefulSet: true`
  - `replicaCount: 3`
  - `resources:`
    - `requests:`
      - `cpu: 500m`
      - `memory: 500Mi`
    - `limits:`
      - `cpu: 1000m`
      - `memory: 1000Mi`
- `api:`
  - `ingress:`
    - `enabled: true`
  - `image: devtube.azurecr.io/devtube-api`
  - `image_tag: 1.0.3`
  - `jwt_key: "example"`
  - `port: 5000`
  - `resources:`
    - `requests:`
      - `memory: 500Mi`
      - `cpu: 500m`
    - `limits:`
      - `memory: 1000Mi`
      - `cpu: 1000m`
  - `autoscaling:`
    - `enabled: true`
    - `replicaCount: 2`
- `client:`
  - `ingress:`
    - `enabled: true`
  - `image: devtube.azurecr.io/devtube-app`
  - `image_tag: 1.0.6`
  - `port: 3000`
  - `resources:`
    - `requests:`
      - `memory: 500Mi`
      - `cpu: 500m`
    - `limits:`
      - `memory: 1000Mi`
      - `cpu: 1000m`
  - `autoscaling:`
    - `enabled: true`
    - `replicaCount: 2`
