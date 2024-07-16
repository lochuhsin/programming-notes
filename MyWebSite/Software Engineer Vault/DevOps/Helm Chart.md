---
created: 2024-01-03 10:09
aliases:
  - Chart
  - chart
tags: 
card link:
  - "[[Helm]]"
source:
---
## Description
---

Helm chart is the base of everything. To create a local chart, there are three steps.

```text  
MyChart/  
	Chart.yaml  
	values.yaml  
	templates/  
		 all kubernetes resource. i.e pods, deployments  
```

The “templates” folder contains all definitions of Kubernetes resources. The “values.yaml” defines all the parameters, like numbers, URLs which used in templates. As for the “Chart.yaml” defines the names, types, dependencies, and chart version. Basic information of the local chart.

The interesting part is the dependencies. “Dependencies”, similar to Docker Hub, allow users to add others public charts and deploy together. Just like docker-compose using other official image and combined multiple images together and run it.

By using helm syntax, YAML files, under “templates” folder, are able to access the value under “values.yaml”.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ .Release.Name }}-{{ .Values.backend.deployment.normal.name }}
spec:
  replicas: {{ .Values.backend.deployment.normal.replicas }}
  selector:
    matchLabels:
      app: {{ .Release.Name }}-{{ .Values.backend.deployment.normal.name }}
  template:
    metadata:
      labels:
        app: {{ .Release.Name }}-{{ .Values.backend.deployment.normal.name }}
    spec:
      {{- if .Values.imagePullSecretName }}
      imagePullSecrets:
        - name: {{ .Values.imagePullSecretName }}
      {{- end }}
      containers:
        - name: {{ .Values.backend.deployment.normal.name }}
          image: "{{ .Values.acr }}/backend:{{ .Values.version }}"
          command:
            - /start_wsgi_production
          env:
            - name: HOST_IP
              valueFrom:
                fieldRef:
                  fieldPath: status.hostIP
            - name: GUNICORN_MODE
              value: {{ .Values.backend.deployment.normal.gunicornMode }}
```

The above code is an example of using brackets {{}} to access the values.

After this, using `helm install or helm upgrade` for further steps. Of course, we could use public charts and overwrite with our values. Then we don’t need the “templates” and “Chart.yaml”. Just define “values.yaml” and run the following command.

- `helm install --values values.yaml -n monitor loki grafana/loki`
- `helm upgrade --values values.yaml -n monitor loki grafana/loki`  
Using “grafana/loki” as example

## Reference
---





