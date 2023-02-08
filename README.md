# Deploy-Promethes-and-Grafana-on-OCI-OKE

    
Login to OCI console


From the OCI Services menu(top left hambuger buttton), click Developer Services > Kubernetes Clusters (OKE).


Under List Scope, select the compartment in which you would like to create a cluster. Click Create Cluster.

Click Create Cluster

Choose Quick Create and click Submit.

Fill out the Cluster details:

        Name: Provide a name 
        Compartment: Choose your compartment
        Kubernetes Version: Choose the most recent version(At the time of making this tutorial,the most recent version is v1.25.4)
        Kubernetes API Endpoint: Public Endpoint
        Kubernetes Worker Nodes: Private Workers
        Shape and Image: Select a pod shape, Number of OCPUS, Amount of RAM and Image based on your requirement (VM.Standard.E4.Flex, 2 OCPU and 8GB Ram will be used in this example)
        Node count: Provide number of nodes(3 in this example)

    Click Next

    Click "Create Cluster" after reviewing your details


Accesss the cluster



kubectl create namespace monitoring

kubectl get namespaces




helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add stable https://kubernetes-charts.storage.googleapis.com/
helm repo update



helm install prom --namespace monitoring  prometheus-community/kube-prometheus-stack


kubectl edit svc prom-grafana -n monitoring


Add a public LB annotation
apiVersion: v1
kind: Service
metadata:
  annotations:
    oci.oraclecloud.com/load-balancer-type: "lb"





type: LoadBalancer

