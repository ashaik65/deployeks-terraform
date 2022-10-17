# Learn Terraform - Provision an EKS Cluster

This repo is a companion repo to the [Provision an EKS Cluster learn guide](https://learn.hashicorp.com/terraform/kubernetes/provision-eks-cluster), containing
Terraform configuration files to provision an EKS cluster on AWS.


Run the following command to retrieve the access credentials for your cluster and configure kubectl.

aws eks --region $(terraform output -raw region) update-kubeconfig \
    --name $(terraform output -raw cluster_name)

So it will update the kubeconfig file for us and now we can do kubectl to see our nodes


# Verify the Cluster

Use kubectl commands to verify your cluster configuration.

First, get information about the cluster.

kubectl cluster-info

Kubernetes control plane is running at https://128CA2A0D737317D36E31D0D3A0C366B.gr7.us-east-2.eks.amazonaws.com
CoreDNS is running at https://128CA2A0D737317D36E31D0D3A0C366B.gr7.us-east-2.eks.amazonaws.com/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.

Notice that the Kubernetes control plane location matches the cluster_endpoint value from the terraform apply output above.

Now verify that all three worker nodes are part of the cluster.

                   kubectl get nodes
                               NAME                                       STATUS   ROLES    AGE   VERSION
                               ip-10-0-1-79.us-east-2.compute.internal    Ready    <none>   91m   v1.22.9-eks-810597c
                               ip-10-0-2-107.us-east-2.compute.internal   Ready    <none>   92m   v1.22.9-eks-810597c
                               ip-10-0-3-176.us-east-2.compute.internal   Ready    <none>   91m   v1.22.9-eks-810597c
  
  
  
