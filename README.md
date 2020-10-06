# a CI/CD pipeline to set WLS domain on Oracle k8s operator

# How to install Operator , provided Helm and kubectl are installed and set up to interact with your cluster. 

$ kubectl create namespace sample-weblogic-operator-ns

$ kubectl create serviceaccount -n sample-weblogic-operator-ns sample-weblogic-operator-sa

$ helm repo add weblogic-operator https://oracle.github.io/weblogic-kubernetes-operator/charts

$ helm repo update

$ helm install sample-weblogic-operator weblogic-operator/weblogic-operator  --namespace sample-weblogic-operator-ns   --set serviceAccount=sample-weblogic-operator-sa   --set "domainNamespaces={}"   --wait

Once you have installed the operator you need to tell it what namedpaces to manage. So if you're going to deploy your domain to the sample-domain1-ns namespace then:

$ helm upgrade   --reuse-values   --set "domainNamespaces={sample-domain1-ns}"   --wait   sample-weblogic-operator   kubernetes/charts/weblogic-operator

