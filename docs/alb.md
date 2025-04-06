# 🌐 AWS ALB Controller Setup

To expose the application to the external world, we need to configure an **AWS Application Load Balancer (ALB)** using the **AWS Load Balancer Controller**.
---

## 🧾 Step 1: Download IAM Policy
```
curl -O https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.11.0/docs/install/iam_policy.json
```

## 🧾 Step 2: Create IAM Policy
```
aws iam create-policy \
    --policy-name AWSLoadBalancerControllerIAMPolicy \
    --policy-document file://iam_policy.json
```

## 🧾 Step 3: Create IAM Role & Service Account
```
eksctl create iamserviceaccount \
  --cluster=<your-cluster-name> \
  --namespace=kube-system \
  --name=aws-load-balancer-controller \
  --role-name AmazonEKSLoadBalancerControllerRole \
  --attach-policy-arn=arn:aws:iam::<your-aws-account-id>:policy/AWSLoadBalancerControllerIAMPolicy \
  --approve
```
**Note**: Here you should update your cluster name and account_id

![Create IAM role](images/createiamrole.png)
