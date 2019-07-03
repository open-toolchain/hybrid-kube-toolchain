# ![Icon](./.bluemix/secure-lock-kubernetes.png) Develop a Kubernetes app in hybrid cloud


### Develop a secure Docker app in public Cloud for staging and private Cloud for production 
This Hello World application uses Docker with Node.js and includes a DevOps toolchain that is preconfigured for continuous delivery with Vulnerability Advisor, source control, issue tracking, and online editing, and staging deployment to the IBM Cloud Kubernetes Service (IKS) and final production deployment to IBM Cloud Private (ICP).

![Icon](./.bluemix/toolchain.png)

Application code is stored in source control, along with its Dockerfile and its Kubernetes deployment script.
The target cluster is configured during toolchain setup (using a IBM Cloud API key and cluster name). You can later change these by altering the Delivery Pipeline configuration.
Any code change to the Git repo will automatically be built, validated and deployed into Kubernetes clusters.

![Icon](./pipeline.png)

### Prerequisites

#### Using IBM Cloud Private (ICP)
You need to get a non expiring token to deploy continuously into your ICP cluster. 
Here are steps to do so using a permanent service account token (see [also](https://www.ibm.com/developerworks/community/blogs/fe25b4ef-ea6a-4d86-a629-6f87ccf4649e/entry/Configuring_the_Kubernetes_CLI_by_using_service_account_tokens1?lang=en)).
- Log in to your private cluster management console. Also see [Accessing your IBM® Cloud Private cluster by using the management console](https://www.ibm.com/support/knowledgecenter/SSBS6K_2.1.0/manage_cluster/cfc_gui.html?view=kc).
- Select User Name > Configure client, which is in the upper right of the window.
- Copy and paste the configuration information to your command line, and press Enter
- Create target namespace in ICP console if not already existing, either in ICP console or command line: 
```
CLUSTER_NAMESPACE=prod
kubectl create namespace ${CLUSTER_NAMESPACE}
```
- Either create a specific serviceaccount in ICP, or leverage the existing `defaultserviceaccount` as instructed below to retrieve its token
```
SERVICE_ACCOUNT_NAME=default
SECRET_NAME=$(kubectl get sa "${SERVICE_ACCOUNT_NAME}" --namespace="${CLUSTER_NAMESPACE}" -o json | jq -r .secrets[].name)
SERVICE_ACCOUNT_TOKEN=$(kubectl get secret ${SECRET_NAME} --namespace ${CLUSTER_NAMESPACE} -o jsonpath={.data.token} | base64 -D)
echo ${SERVICE_ACCOUNT_TOKEN}
```
- Ensure admin permission for chosen service account in specific namespace:
```
# grant admin permission (rbac)
kubectl create clusterrolebinding cd-admin --clusterrole=admin --serviceaccount=${CLUSTER_NAMESPACE}:${SERVICE_ACCOUNT_NAME} 
```
- Copy and save the value of `SERVICE_ACCOUNT_TOKEN`, it will be needed for later configuring pipeline in IBM Cloud public

### To get started, click this button:
[![Create toolchain](https://cloud.ibm.com/devops/graphics/create_toolchain_button.png)](https://cloud.ibm.com/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fhybrid-kube-toolchain&env_id=ibm:yp:us-south)

### Tutorial steps
1. Setup this hybrid toolchain demonstrating how to build/test in IKS and deploy into private cluster (e.g. ICP)
2. See 'prod' deploy failing because cannot connect from IBM Cloud public into private cluster target
3. Setup a pipeline private worker in that ICP cluster
4. Re-run the pipeline and see the prod deployment stage succeeding

---
### Learn more 

* Blog [Continuously deliver your app to Kubernetes with IBM Cloud](https://www.ibm.com/blogs/bluemix/2017/07/continuously-deliver-your-app-to-kubernetes-with-bluemix/)
* Step by step [tutorial](https://www.ibm.com/devops/method/tutorials/tc_hybrid_kube)
* [Getting started with IBM Cloud Kubernetes](https://cloud.ibm.com/docs/containers?topic=containers-getting-started)
* [Getting started with IBM Cloud Private](...)
* [Getting started with toolchains](https://cloud.ibm.com/devops/getting-started)
* [Documentation](https://cloud.ibm.com/docs/services/ContinuousDelivery/index.html?pos=2)
