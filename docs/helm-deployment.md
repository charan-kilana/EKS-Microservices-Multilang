## 🧰 Helm Chart Installation – Robot Shop

Use this Helm chart to customize your install of the **Robot Shop** application.

### For Helm v2.x:
```bash
helm install --name robot-shop --namespace robot-shop .
```

### For Helm v3.x:
```bash
kubectl create ns robot-shop
helm install robot-shop --namespace robot-shop .
```

> **Note:**  
> You should clone the repository and navigate to the path:  
> `/root/EKS-Microservices-Multilang/EKS/helm`  
> This directory must contain both `Chart.yaml` and `values.yaml` in order to install the Helm release `robot-shop` successfully.

![Helm Chart Directory Structure](images/default_path_helm.png)
