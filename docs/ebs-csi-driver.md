## 📦 Why Add the EBS CSI Plugin to the EKS Cluster?

The **Amazon EBS CSI (Container Storage Interface) plugin** is required in EKS to enable Kubernetes to manage **Amazon EBS volumes** as persistent storage for stateful workloads.

### ✅ Key Reasons:

- **Persistent Storage for Pods**: Allows your pods (like Redis, MySQL, etc.) to request and attach EBS volumes dynamically using PersistentVolumeClaims (PVCs).
- **Stateful Workloads Support**: Essential for StatefulSets that need stable, durable storage even if pods restart or move.
- **Separation of Concerns**: CSI drivers decouple storage logic from core Kubernetes, enabling better portability and maintainability.
- **AWS Best Practice**: Amazon recommends using the EBS CSI driver instead of the in-tree volume plugin (which is deprecated).

### 🧠 Real Use Case in This Project:

We're deploying **Redis** as a StatefulSet, which requires a **PersistentVolume** to store cart/session data.  
To allow Redis pods to attach EBS volumes, the **EBS CSI plugin must be installed** and configured on the EKS cluster.

# 📦 EBS CSI Plugin Configuration

The Amazon EBS CSI (Container Storage Interface) plugin enables Kubernetes running on EKS to manage Amazon EBS volumes for persistent storage.

To work correctly, the EBS CSI plugin requires **IAM permissions** to make calls to AWS APIs on your behalf.

---

## ✅ Step 1: Create IAM Role and Attach Policy


Replace `<YOUR-CLUSTER-NAME>` with your actual EKS cluster name:

```bash
eksctl create iamserviceaccount \
    --name ebs-csi-controller-sa \
    --namespace kube-system \
    --cluster <YOUR-CLUSTER-NAME> \
    --role-name AmazonEKS_EBS_CSI_DriverRole \
    --role-only \
    --attach-policy-arn arn:aws:iam::aws:policy/service-role/AmazonEBSCSIDriverPolicy \
    --approve
```

## ✅ Step 2: Run the following command. Replace with the name of your cluster, with your account ID.
```bash
eksctl create addon --name aws-ebs-csi-driver --cluster <YOUR-CLUSTER-NAME> --service-account-role-arn arn:aws:iam::<AWS-ACCOUNT-ID>:role/AmazonEKS_EBS_CSI_DriverRole --force
```
