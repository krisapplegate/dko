## Challenge
Install vcluster to test upgrades (eg. 1.20 to 1.21 DOKS version) of your cluster. With a virtual cluster, you can create a new Kubernetes cluster inside your existing DOKS cluster, test the application in this new vcluster, and then upgrade your original cluster if everything works well with the new version.

## Procedures
After setting up my account and installing the doctl command line (via brew), I was off to get started with getting the infrastrcuture stood up.

First, I created a cluster using the following:
```bash
doctl kubernetes cluster create do-kapplegate --version 1.20.11-do.0  --region nyc1
```
This gives me 3 nodes at a version that I can upgrade from (to 1.21 later in the evaluation).

Normally I'd now need to grab the kubeconfig so that I can interact w/ the cluster from kubectl. However, it looks like that's included in the CLI command above (nice QoL feature). If I did need it, I could grab the config and add it to my local kubeconfig with:
```bash
doctl kubernetes cluster kubeconfig save do-kapplegate
```

One other shortcut I do to help with CLI interactions w/ kubectl is to alias it to `k`:
```bash
alias k=kubectl
```

Now I can check that I can see the cluster from the cli
```bash
k get nodes
NAME                               STATUS   ROLES    AGE     VERSION
do-kapplegate-default-pool-ubqz2   Ready    <none>   4m33s   v1.20.11
do-kapplegate-default-pool-ubqzl   Ready    <none>   2m35s   v1.20.11
do-kapplegate-default-pool-ubqzt   Ready    <none>   2m47s   v1.20.11
```
