

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: special-config
  namespace: als
data:
  LOCATION: '<YOUR_LOCATION>'
  PUBLIC_IPV4: '<YOUR_PUBLIC_IP>'
  SPEEDTEST_FILE_LIST: '1MB 10MB'
  DISPLAY_TRAFFIC: 'false'
  UTILITIES_FAKESHELL: 'false'
  UTILITIES_IPERF3: 'false'
```

```
kubectl apply -f manifests/k8s/deployment.yaml
kubectl create secret generic special-config -n als \
  --from-literal=LOCATION='<YOUR_LOCATION>m' \
  --from-literal=PUBLIC_IPV4='<YOUR_PUBLIC_IP>' \
  --from-literal=SPEEDTEST_FILE_LIST='1MB 10MB' \
  --from-literal=DISPLAY_TRAFFIC='false' \
  --from-literal=UTILITIES_FAKESHELL='false' \
  --from-literal=UTILITIES_IPERF3='false' \
  --dry-run=client -o yaml | kubectl apply -f - && kubectl rollout restart deployment
```