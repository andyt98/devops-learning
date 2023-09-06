To create the EKS Cluster on AWS
```
eksctl create cluster --name demo-cluster --version 1.20 --region eu-central-1 --nodegroup-name demo-nodes --node-type t2.micro --nodes 2 --nodes-min 1 --nodes-max 3
```

On Jenkins server
- install kubectl
- install aws cli

Run commands:
```
aws configure
aws eks update-kubeconfig --region region-code --name my-cluster
```