# Layer 4 Services

## Services are layer 4 constructs

- you can assign IP addresses to services, but they are still layer 4
    (ie a service is not an IP address it is an IP address + protocol + port)
- This is caused by the current implementation of `kube-proxy`
    it relies on mechanism that do not support layer 3
-  as a result: you have toi indicate the port number for your service
-  running services with arbitrary port (or port ranges) requires hacks (eg host networking mode)


 