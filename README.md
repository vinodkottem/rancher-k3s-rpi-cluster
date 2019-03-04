# rancher-k3s-rpi-cluster

## Running Light weight Kubernetes(https://k3s.io/) on raspberry pi's

### Requirements

1. 2 raspberry pi's (used 3b+ models)


####  1. Setting up Master Node

1. Run the following command to install k3s on a pi which is going to be master. By default it enables a systemd for to run k3s in server mode. 

```bash
curl -sfL https://get.k3s.io | sh -
```

2. Run the following command to see services are up and running.

```bash
sudo k3s kubectl get node
```

3. Get "NODE_TOKEN" from /var/lib/rancher/k3s/server/node-token on your master node which is used to join agents.

```bash
sudo cat /var/lib/rancher/k3s/server/node-token
```

####  2. Setting up Agent on another Pi

1. Manually install k3s in worker node & run k3s in agent mode instead of server.
2. Run agent

```bash
sudo k3s agent --server https://<IP ADDRESS OF MASTER>:6443 --token ${NODE_TOKEN}
```

####  3. To access cluster from outside.

1. Copy the /etc/rancher/k3s/k3s.yaml from master to local machine/laptop.

2. Replace "localhost" with the IP of the master in the localfile.

3. Set the KUBECONFIG on terminal.

```bash
export KUBECONFIG=/Users/vinodk/.kube/rancher-k3s.yaml
```
4. Run the following command to see you are able to access the cluster

```bash
kubectl get node
```





