# helmfile 

## Prerequisites 

  * helmfile (binary)
  * helm-diff

## After installation of binary

```
helmfile init --force
```

## Create helmfile.yaml 

```
# toplevel
cd
nano helmfile.yaml
```

```
repositories:
- name: prometheus-community
  url: https://prometheus-community.github.io/helm-charts

releases:
- name: prom-norbac-ubuntu
  namespace: prometheus
  chart: prometheus-community/prometheus
  set:
  - name: rbac.create
    value: false
- name: jochenapp1
  namespace: app1
  chart: app1
```

```
helmfile apply
```


## Reference 

  * https://github.com/helmfile/helmfile
