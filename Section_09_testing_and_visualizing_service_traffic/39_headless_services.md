# Headless Services


## IF we do not need a load balancer

- sometimes, we want to access our scaled services directly:
  - if we want toi save a tiny little bit of latency (typically less than 1ms)
  - if we need to connect over artibtrary ports (instead of a few fixed ones)
  - if we need to communicate over another protocol than UDP or TCP
  - if we want to decide how to balance the requests client-side

- in that case we can use a headless service

## Headless Services

- A headless service is obtained by setting the `clusterIP` field to `None`
  - Either with --cluster-ip=None or by providing a custom YAML
- as a result, the service does not have a virtual IP address
- since there is no virtual IP address there is no load balancer either
- core DNS will return the pods' IP addresses as multiple `A` records
- this gives us an easy way to discover all the replicas for a deployment


[this is DNS multi address situation <--- interesting]



Links:
https://kubernetes.io/docs/concepts/services-networking/service/#why-not-use-round-robin-dns
https://kubernetes.io/docs/concepts/services-networking/service/#headless-services