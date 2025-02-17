# Install Seldon Core on EKS via AWS MarketPlace

 * Subscribe to Seldon Core on [AWS MarketPlace](https://aws.amazon.com/marketplace/seller-profile?id=cec67450-7a7e-43d5-8e5f-61e94e7c9e03&ref=dtl_B07KCNBCHV) and retrieve the log in command to authenticate your Docker client.

 (Note: below is for the 0.5.0 release and will differ for other releases).
  ```
  $(aws ecr get-login --no-include-email --region us-east-1 --registry-ids 403495124976)
  ```
 
 * [Create your EKS cluster and authenticate kubectl](https://docs.aws.amazon.com/eks/latest/userguide/getting-started.html).
   Configure local Kubectl
  ```
  aws eks --region <CLUSTER_REGION> update-kubeconfig --name <CLUSTER-NAME>
  ```
 
 * Install [helm](https://docs.helm.sh/) on your cluster if it is not there already.
  ```
  kubectl -n kube-system create sa tiller
  kubectl create clusterrolebinding tiller --clusterrole cluster-admin --serviceaccount=kube-system:tiller
  helm init --service-account tiller
  ```
 
 * Install Seldon Core for the release you subscribed to on Amazon MarketPlace:

For **Seldon 0.5.0**

 ```
  helm install seldon-core-aws --name seldon-core --repo https://storage.googleapis.com/seldon-aws-charts --version 0.5.0
  helm install stable/ambassador --name ambassador --set crds.keep=false
 ```

For **Seldon 0.2.6**

 ```
   helm install seldon-core-aws --name seldon-core --repo https://storage.googleapis.com/seldon-aws-charts --version 0.2.6
 ```

For **Seldon 0.2.4**

 ```
   helm install seldon-core-aws --name seldon-core --repo https://storage.googleapis.com/seldon-aws-charts --version 0.2.4
 ```


For **Seldon 0.2.3**

 ```
   helm install seldon-core-aws --name seldon-core --repo https://storage.googleapis.com/seldon-aws-charts --version 0.2.3
 ```

# Next Steps

For next steps on using Seldon Core and deploying your first ML models visit the [Seldon Core project page](https://github.com/SeldonIO/seldon-core).

**Note at present you will need to use Ambassador as ingress for the APIs exposed**

# FAQs

## Install a particular version

Use the helm ```--version``` tag to install a particular version, e.g.:

 ```
   helm install seldon-core-aws --name seldon-core --repo https://storage.googleapis.com/seldon-aws-charts \
        --version 0.2.3
 ```

## Install in a particular namespace

Use the helm ```--namespace``` argument to install in a particular namespace


 ```
   helm install seldon-core-aws --name seldon-core --repo https://storage.googleapis.com/seldon-aws-charts \
        --namespace my-namespace
 ```
