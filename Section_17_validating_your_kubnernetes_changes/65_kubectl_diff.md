# Kubectl Diff

- kubernetes 1.13 also introduced `kubectl diff`
- `kubectl diff` does a server-side dry run and shows differences

exercise:
try `kubectl diff` on a simple pod yaml:

curl -o https://k8smastery.com/just-a-pod.yaml
kubectl apply -f just-a-pod.yaml
edit the image tag to :1.17
kubectl diff -f just-a-pod.yaml
