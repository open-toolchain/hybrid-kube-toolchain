# ![Icon](./.bluemix/secure-lock-kubernetes.png) Develop a Kubernetes app with hybrid cloud


### Continuously deliver a secure Docker app in both public Cloud for staging and private Cloud for production 
This Hello World application uses Docker with Node.js and includes a DevOps toolchain that is preconfigured for continuous delivery with Vulnerability Advisor, source control, issue tracking, and online editing, and staging deployment to the IBM Cloud Kubernetes service and final production deployment to IBM Cloud Private.

Application code is stored in source control, along with its Dockerfile and its Kubernetes deployment script.
The target cluster is configured during toolchain setup (using a IBM Cloud API key and cluster name). You can later change these by altering the Delivery Pipeline configuration.
Any code change to the Git repo will automatically be built, validated and deployed into Kubernetes clusters.

![Icon](./.bluemix/toolchain.png)

### To get started, click this button:
[![Create toolchain](https://cloud.ibm.com/devops/graphics/create_toolchain_button.png)](https://cloud.ibm.com/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fhybrid-kube-toolchain&env_id=ibm:yp:us-south)
---
### Learn more 

* Blog [Continuously deliver your app to Kubernetes with IBM Cloud](https://www.ibm.com/blogs/bluemix/2017/07/continuously-deliver-your-app-to-kubernetes-with-bluemix/)
* Step by step [tutorial](https://www.ibm.com/devops/method/tutorials/tc_hybrid_kube)
* [Getting started with IBM Cloud Kubernetes](https://cloud.ibm.com/docs/containers?topic=containers-getting-started)
* [Getting started with IBM Cloud Private](...)
* [Getting started with toolchains](https://cloud.ibm.com/devops/getting-started)
* [Documentation](https://cloud.ibm.com/docs/services/ContinuousDelivery/index.html?pos=2)
