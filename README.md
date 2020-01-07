# Helm Chart

As per: https://docs.bitnami.com/kubernetes/how-to/create-your-first-helm-chart/

## Step 1. Generate Your First Chart

`helm create mychart`

Helm will create a new directory in your project called mychart with the structure shown below.

```
mychart
|-- Chart.yaml
|-- charts
|-- templates
|   |-- NOTES.txt
|   |-- _helpers.tpl
|   |-- deployment.yaml
|   |-- ingress.yaml
|   `-- service.yaml
`-- values.yaml
```

**We can do a dry-run of a helm install and enable debug to inspect the generated definitions:**

with a **--generate-name** flag

`helm install --generate-name --dry-run --debug ./mychart`

with a **name**

`helm install miguel --dry-run --debug ./mychart`

## Step 2. Deploying Your First Chart

The chart you generated in the previous step is setup to run an NGINX server exposed via a Kubernetes Service. By default, the chart will create a ClusterIP type Service, so NGINX will only be exposed internally in the cluster. To access it externally, we’ll use the NodePort type instead.

`helm install example3 ./mychart --set service.type=NodePort`

**Note**: `--set service.type=NodePort` overrides the value found on line# 34 in the `values.yaml`

```
service:
  type: ClusterIP
```

**YOU MUST FORWARD THE PORT IN ORDER TO SEE IT BROWSER**

`kubectl port-forward svc/example3-mychart 7000:80`

So now you have access to the cluster via: http://localhost:7000
