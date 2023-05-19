Remember CoreDNS for Service DNS Resolution
Earlier I talked about CoreDNS being an optional, but necessary thing, inside your Kubernetes cluster. 
Until now, you wouldn't have needed it, because we haven't used DNS inside the cluster to find Services yet. 
One of the jobs for a Service resource is to create the DNS name for the Service IP, 
which then makes something like httpenv resolvable on the Pod networks.

That means that you need to ensure CoreDNS is running before we continue.

If you are using Docker Desktop or minikube, DNS is running out-of-the-box. All done :)

But if you're using MicroK8s, DNS needs to be enabled manually with the command microk8s.
enable dns so that it'll setup and start CoreDNS. 
If you're using MicroK8s you can also see my recommended setup and config slides for it (same from Section 2) here.