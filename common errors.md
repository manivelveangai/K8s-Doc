# Common error in control plan 

## Ex: The connection to the server 10.10.0.0:6443 refused
### Solution:
- Verify the kubeapi and other services in control plane is running on the server by running 
- Verify the logs by running crictl ps -a | grep api it show the exited container and run crictl logs kube-apiserver to verify the logs and also cd /var/logs/containers/
- crictl ps 
- cirtl ps | grep api
- go to /etc/kubernetes/manifests/
- verify the kube-api server yaml file and validate the entries are correct in the yaml file and verify the kubectl get nodes 

## Ex: Connection to the localhost 8080 was refused
### Solution
- Verify the kube-apiserver is running on the control plane, if it's running it might be network or configuration issues 
- Verify the kubeconfiguration file location and make sure it's valid.
- Default kube config file location is $HOME/.kube "export kubeconfig=/tmp/config" 
- copy the kube config file from /etc/kubernetes/admin.conf or use kubectl get nodes --kubeconfig admin.conf to run the temprorarily with admin.conf file 
- export KUBECONFIG=$HOME/.kube/config

## Ex: Pods are going to Pending state: 
### Solution:
- Scheduler is responsible for scheduling the pod verify the scheduler is running on the control plane kubectl get pod -n kube-system. 
- kubectl logs kube-scheduler -n kube-system or kubectl describle kube-scheduler -n kube-system to identify the logs
- verify the mainfest yaml file for the kube-scheduler and make sure the image version is valid

## Ex: Deployment or Replicas issue when deleting the pods in the deployment it won't created the pod similar to the replication sets.
### Solution:
- kube-controller is responsible for creating the replication set as per the definition 
- verify the kube controller status kubectl get pod -n kube-system 
- run kubectl logs or kubectl describe pod to get the status of the kubectonrller 
- Verify the kube-controller mainfest file and make sure the configuration parameters informations are valid
      kubectl cluster-info
  [Troubleshooting Clusters] (https://kubernetes.io/docs/tasks/debug/debug-cluster/)
  [Debugging Kubernetes nodes with crictl] (https://kubernetes.io/docs/tasks/debug/debug-cluster/)
    
