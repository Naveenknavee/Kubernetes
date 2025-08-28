Node port troubeshoot 


$ minikube service nginx-service
|-----------|---------------|-------------|---------------------------|
| NAMESPACE |     NAME      | TARGET PORT |            URL            |
|-----------|---------------|-------------|---------------------------|
| default   | nginx-service |          80 | http://192.168.49.2:30001 |
|-----------|---------------|-------------|---------------------------|
* Starting tunnel for service nginx-service.
|-----------|---------------|-------------|------------------------|
| NAMESPACE |     NAME      | TARGET PORT |          URL           |
|-----------|---------------|-------------|------------------------|
| default   | nginx-service |             | http://127.0.0.1:57267 |
|-----------|---------------|-------------|------------------------|
* Opening service default/nginx-service in default browser...
! Because you are using a Docker driver on windows, the terminal needs to be open to run it.
* Stopping tunnel for service nginx-service.

✅ Why NodePort works on AWS nodes

In AWS EKS, each Kubernetes node is an EC2 instance with a real public IP.

A NodePort service opens the specified port (e.g., 30001) on all nodes in the cluster.

When you hit http://<node-public-ip>:30001, AWS routes it directly to that node and forwards traffic to your Pod.

✅ Why it doesn’t work on Minikube

Minikube runs inside a VM or container on your laptop.

The NodePort (30001) is open inside the Minikube VM, not on your host machine.

Your host OS doesn’t expose Minikube’s internal networking by default.

That’s why you need:

minikube ip + nodePort

or minikube service command (which creates a proxy
