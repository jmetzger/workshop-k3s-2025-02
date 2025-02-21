# Install mailpit 

## Walkthrough 

```
helm repo add jouve https://jouve.github.io/charts/
helm -n smtp upgrade --create-namespace --install smtp-server jouve/mailpit
```

## Also include Ingress 

```
nano values.yaml
```

```
ingress:
   enabled: true
   hostname: mailpit.jochen.t3isp.de
   ingressClassName: nginx 
```

```
helm -n smtp upgrade --create-namespace --install smtp-server jouve/mailpit -f values.yaml
```
