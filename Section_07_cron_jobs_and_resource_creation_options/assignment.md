1 How many nodes does your cluster have?
(the answer should be the kubectl command you used to get the answer)

We can get a list of nodes with kubectl get nodes.

2 What kernel version and what container engine is each node running?
(the answer should be the kubectl command you used to get the answer)

kubectl get nodes -o wide will list extra information for each node.   

3 . List only the pods in the kube-system namespace.
(the answer should be the kubectl command you used to get the answer)

kubectl get pods --namespace=kube-system

4 Explain the role of some of these pods.

This depends on how our cluster was set up.                                                                                       

On some clusters, we might see pods named etcd-XXX or kube-apiserver-XXX. these correspond to control plane components.             

It's also common to see kubedns-XXX or coredns-XXX. These implement the DNS service that lets us resolve service names into their service IP's.

5 If there are few or no pods in kube-system, why could that be?

On some clusters, the control plane is located outside the cluster itself, and not running as containers.                                                   

In that case, the control plane won't show up in kube-system, but you can find on host with ps aux | grep kube.

6 Create a deployment using kubectl create that runs the image bretfisher/clock and name it ticktock.
(the answer should be the kubectl command you used)

kubectl create deployment ticktock --image=bretfisher/clock

By default, it will have one replica, translating to one container.

7 Increase the number of pods running in that deployment to three.
(the answer should be the kubectl command you used)

kubectl scale deployment ticktock --replicas=3

This will scale the deployment to three replicas (two more containers).

8 Use a selector to output only the last line of logs of each container.
(the answer should be the kubectl command you used)

kubectl logs --selector=app=ticktock --tail=1

All the resources created with kubectl create deployment xxx will have the label app=xxx.                                         

If you needed to use a pod selector, you can see them in the resource spec that created them.

In this case that's the ReplicaSet, so kubectl describe replicaset ticktock-xxxxx would help.