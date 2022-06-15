# Despliegue de IDS en kubernetes

In this repository is everything to deploy an IDS system with Kubernetes. A brief description of these systems according to the official site  [oficial](https://internationaldataspaces.org/) *A secure, sovereign system of data sharing in which all participants can realize the full value of their data"*. 

## Requisites
This section summarizes the hardware and software features used for the deployment. Note that the IDS is sensitive to traffic load and may require a more powerful hardware system if traffic increases.

### Software-requirements

- [Kubectl](https://kubernetes.io/es/docs/tasks/tools/) version:
  - Client Version: v1.24.0
  - Kustomize Version: v4.5.4
  - Server Version: v1.24.0
- [Kompose](https://kompose.io/)
  - 1.26.0

- Cluster runs in [Docker-Desktop](https://docs.docker.com/desktop/windows/install/)
  - v20.10.14

-  [IDS-Release 1.0](https://github.com/International-Data-Spaces-Association/IDS-testbed)
-   OS Windows 10 Enterprise
    -   WSL2: Ubuntu 20.04 LTS

### Hardware-requirements
- 16 GB RAM memory
- Intel(R) Core(TM) i5-10310U CPU @ 1.70GHz   2.21 GHz

- 237 GB ROM memory

## Architecture

The following figure shows the proposed architecture. 

![figura](./pictures/Testbed_1.0.png)

The main parts of the system are:
- 
-  [IDS connectors](https://international-data-spaces-association.github.io/DataspaceConnector/) have been used to develop the A and B connectors. This connector sends data to a device or database in a certified and trusted environment. Thus, the data providers always have control over their data. 
  
- Un Dynamic Attribute Provisioning Service" [DAP](https://github.com/International-Data-Spaces-Association/IDS-G/blob/main/Components/IdentityProvider/DAPS/README.md)  DAPS aims to verify and secure a set of attributes of organizations and connectors. In this way, third parties need only rely on the DAPS assertions. This DAPS system uses Omejdn instances to perform the confirmations and store the certificates. 
  
- Un [broker](https://github.com/International-Data-Spaces-Association/metadata-broker-open-core)The IDS Metadata Broker is one of the modules still under development and intends to help IDSA members implement custom broker solutions.

## Starting the architecture

- The first step is to created a namespace.
  
  `kubectle create namespace ids-2`
  

- It is necessary to install an Nginx driver to be able to make the calls to the cluster from the outside. If the Ingress-Nginx repo is not updated, in this [link](https://kubernetes.github.io/ingress-nginx/deploy/) is the official documentation

    `kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.2.0/deploy/static/provider/cloud/deploy.yaml`

- The next step would be to launch the application manifests.

    `kubectl apply -f export -n ids-2`

- The last point would be to check that the deployment has been performed successfully. Using tools such as [K9s](https://k9scli.io/), the result should be as below.
    
![figura](./pictures/pods_running.png)



Finally, with a tool such as [Postman](https://www.postman.com/), a test could be performed to verify that the communication and connectivity of the infrastructure are correct. For this purpose, the [ids-certification-testing](TestbedPreconfiguration.postman_collection.json) file is used, in which a set of tests verifies the tool's proper operation in Kubernetes.