https://sadservers.com/scenario/buenos-aires

Add verb "get" to logshipper-cluster-role.

    1  export k=kubectl
    2  k get pods -n
    3  kubectl
    4  kubectl --version
    5  alias k=kubectl
    6  k get pods
    7  k --version
    8  k version
    9  sudo k version
   10  sudo kubectl version
   11  sudo kubectl get pods 
   12  sudo kubectl describe pod logshipper-597f84bf4f-6ssjq
   13  sudo kubectl logs logshipper:v3
   14  sudo kubectl logs logshipper-597f84bf4f-6ssjq 
   15  sudo kubectl auth 
   16  sudo kubectl auth can-i *.*
   17  sudo kubectl auth can-i 
   18  sudo kubectl auth can-i -h
   19  sudo sudo kubectl auth can-i -h
   20  sudo kubectl auth can-i'*' '*' 
   21  sudo kubectl auth can-i '*' '*'
   22  sudo kubectl get serviceaccount 
   23  sudo kubectl get serviceaccount logshipper-sa -o yaml
   24  sudo kubectl get role 
   25  sudo kubectl get clusterrole
   26  sudo kubectl get clusterrole | grep log
   27  sudo kubectl api-resources
   28  sudo kubectl api-resources | grep cluster
   29  sudo kubectl get clusterrole logshipper-cluster-role 
   30* 
   31  sudo kubectl logs logshipper-597f84bf4f-6ssjq 
   32  sudo kubectl edit clusterrole logshipper-cluster-role 
   33  sudo kubectl get clusterrolebinding 
   34  sudo kubectl get clusterrolebinding  | grep log
   35  sudo kubectl get clusterrolebinding  logshipper-cluster-role-binding -oyaml
   36  sudo kubectl get pods
   37  sudo kubectl delete pods logshipper-597f84bf4f-6ssjq 
   38  sudo kubectl get pods -w
   39  history