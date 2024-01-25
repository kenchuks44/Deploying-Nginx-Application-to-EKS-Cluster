# Deploying-Application-to-EKS-Cluster
In this tutorial, we learn how to deploy a simple nginx application to EKS cluster. To achieve this, we would provision an EKS cluster, create worker nodes, connect the Node Group to EKS cluster and then deploy the nginx application to the EKS cluster

## Step 1: Provision EKS cluster
To provision the cluster, we firstly create IAM role for the cluster, create VPC and then, create the cluster and connect kubectl with the cluster.

# Create IAM role for cluster:
We create IAM role and attach the policy, AmazonEKSClusterPolicy to the cluster role to allow AWS to create and manage components.

![Screenshot (233)](https://github.com/kenchuks44/Deploying-Nginx-Application-to-EKS-Cluster/assets/88329191/2032f238-ff42-4ead-b4ef-a2ccbf219fc6)

![Screenshot (234)](https://github.com/kenchuks44/Deploying-Nginx-Application-to-EKS-Cluster/assets/88329191/477eb50f-59f9-4339-a39a-ffa3c8c3363a)

# Create VPC:
EKS cluster needs specific networking configuration as default VPC is not optimized for it. The VPC created is for the worker nodes. Worker nodes needs specific firewall configuration for master-worker node communication. AWS has a preconfigured template for VPC creation and we will achieve this using CloudFormation. Here, we will create a stack using Amazon S3 URL below:
```
https://s3.us-west-2.amazonaws.com/amazon-eks/cloudformation/2020-10-29/amazon-eks-vpc-private-subnets.yaml
```
![Screenshot (318)](https://github.com/kenchuks44/Deploying-Nginx-Application-to-EKS-Cluster/assets/88329191/b8236e25-9ba2-426b-b10a-1743e1ad6afb)

![Screenshot (236)](https://github.com/kenchuks44/Deploying-Nginx-Application-to-EKS-Cluster/assets/88329191/72c611a6-8daf-42c5-85e4-2acbc84ce2d7)

![Screenshot (235)](https://github.com/kenchuks44/Deploying-Nginx-Application-to-EKS-Cluster/assets/88329191/63e93377-7d17-4e78-961b-5e581b48a694)

# Create EKS cluster

![Screenshot (320)](https://github.com/kenchuks44/Deploying-Nginx-Application-to-EKS-Cluster/assets/88329191/1b718b15-84e3-4dc1-999e-da810628d55f)

![Screenshot (238)](https://github.com/kenchuks44/Deploying-Nginx-Application-to-EKS-Cluster/assets/88329191/f0562cdd-fd67-429b-81d9-1c07fec1e4ac)

# Connect Kubectl to EKS Cluster
Go to terminal to create kubeconfig file by running the commands below:
```
aws configure list
aws eks update-kubeconfig --name <eks-cluster-name>
```

![Screenshot (259)](https://github.com/kenchuks44/Deploying-Nginx-Application-to-EKS-Cluster/assets/88329191/fc03447c-4835-4ce2-9814-60646b16ee98)

![Screenshot (223)](https://github.com/kenchuks44/Deploying-Nginx-Application-to-EKS-Cluster/assets/88329191/30ca8d70-a7ba-47bd-8713-f50a41b10313)

## Step 2: Create Worker Nodes
Firstly, we create IAM role for the Node Group and then, add the Node Group to the EKS cluster

# Create IAM role for Node Group
We create IAM role and attach policies to enable us connect to the EKS cluster, provide read access to EC2 container registry repositories and provide Amazon VPC CNI Plugin (amazon-vpc-cni-k8s) the permissions it requires to modify the IP address configuration on the EKS worker nodes. 

![Screenshot (239)](https://github.com/kenchuks44/Deploying-Nginx-Application-to-EKS-Cluster/assets/88329191/1b88c8cb-4ba2-4421-9654-c474377e2cc2)

![Screenshot (240)](https://github.com/kenchuks44/Deploying-Nginx-Application-to-EKS-Cluster/assets/88329191/8cdcd984-c93c-471f-b6a6-18c5bedd861b)

![Screenshot (242)](https://github.com/kenchuks44/Deploying-Nginx-Application-to-EKS-Cluster/assets/88329191/6ac65498-9c28-4caf-8c8f-b01fc403708f)

![Screenshot (250)](https://github.com/kenchuks44/Deploying-Nginx-Application-to-EKS-Cluster/assets/88329191/2cd08ef4-1130-4a99-89a8-7e289b4c3cca)

With Node Group, all required worker processes (container runtime, kubelet, kubeproxy) will be created














