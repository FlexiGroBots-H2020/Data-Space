# YAML nomenclature <img src="../pictures/img-buildkite/kubernetes.png" width="30" height="30" alt="kubernetes"/>

In order to organise the manifests we have used a name structure for the YAML files. For that, the name file has a number that defines the type of k8s elements. Below it is shown this nomenclature:

  - 0- Service

  - 1- Deployment
  
  - 2- Configmap
  
  - 3- Secret
  
  - 4- Ingress, Ingressroute, IngressrouteTCP
  
  - 5- NetworkPolicy

  - 7- CustomResourceDefinition
  
  - 8- Middleware
  
  - 9- ClusterRole
  
  - 10- PersistanceVolume
