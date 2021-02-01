# Odoo chart

## Usage

1. Create postgresql username and db
2. Create kube namespace (`kubectl create ns CHANGEME_NAMESPACE`) and copy docker-hub pull secret if necessary
3. Create custom values file, for example;

```yaml
imagePullSecrets:
  - name: docker-hub

image:
  repository: "glodouk/odoo"
  tag: "13.0e"

config:
  adminPassword: "CHANGEME"
  postgresql:
    host: "10.150.13.4"
    user: "CHANGEME"
    password: "CHANGEME"

web:
  enabled: true

  ingress:
    enabled: true
    match: Host(`CHANGEME.glodo.cloud`)

queue:
  enabled: false

upgrade:
  enabled: true
```

4. Run `helm install CHANGEME_PROJECTNAME -f myvals.yaml odoo -n CHANGEME_NAMESPACE`