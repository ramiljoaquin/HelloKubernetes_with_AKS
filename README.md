# HelloKubernetes_AKS
Mange Kubernetes with AKS

![Kube architecture][logo]

[logo]: https://github.com/ramiljoaquin/HelloKubernetes_AKS/blob/master/assets/KubeArchitecture.png "Kubernetes architecture"



## Course details
1h 44m  Advanced  Released: 3/27/2019

Kubernetes is quickly becoming the standard for containerized infrastructure. In this course, learn how to use this popular open-source container orchestration engine with Microsoft Azure by leveraging Azure Kubernetes Service (AKS). Instructor Robert Starmer reviews the top options for getting AKS deployed, focusing on deploying the Managed Master model provided by AKS via the 'az' command line client, including integration with the Azure Container registry for more efficient application deployments. He then discusses how to scale AKS workers, create storage classes, and manage AKS deployments, including how to enable aggregate statistics using Azure Monitor.


# Learning objectives
- Deployment models
- Scaling AKS workers
- Setting up nodes
- Using labels to select pools
- Creating storage classes
- Networking options and capabilities
- Load balancing and ingress
- Managing AKS deployments

# Skills covered in this course

KubernetesMicrosoft AzureCloud Computing


## Instructor

Robert Starmer
Cloud Advisor, Founder of Kumulus Technologies


# Requirements for EKS deployment

- [Instructor] In order to leverage the EKS service from Amazon, there are a couple of precursor stages that we have to do. Firstly, we have to set up IAM, the identity and authentication management resources in Amazon, for our EKS environment. 

We have to create the appropriate role that the EKS service is going to use to implement features on our behalf, within our environment. And we also have to create a VPC, specifically for EKS to use. This keeps it separate from all of the other resources that we might try to create in our environments and allows it to have the appropriate network segments and network segmentation needed to apply all of its services. 

Then we can deploy the EKS services themselves. We do this by using the web console, is the easiest way to actually deploy this, and deploying EKS through the web console. You can also do it via the AWS CLI, but the web console is a straightforward way of approaching this. 

We need to establish a set of credentials and there's an authenticator, a specific authenticator application, along with the kubectl Kubernetes command line that need to be installed. And then we need to enable that configuration. And we can do that with the AWS command line, adding our Kubernetes configuration automatically, just by passing in our newly-created cluster name. Or we can also manually create those configuration commands as well. And lastly, we actually add into our control plane, because EKS is really managing the control plane for us, we add our worker nodes. 

We're going to do that with another cloud formation template. And then we need to authenticate those worker nodes into our EKS cluster. And we're going to do that by applying a config map, which is a classic, or rather, standard Kubernetes model for passing in information into the system. That same configuration map is useful for other authentication purposes as well. 

And finally, we just have to wait for our worker nodes to register. That usually only takes 30 to 60 seconds and then we can start using our environment. There is one other thing that you may have to do if you haven't done it already, and that is make sure that you've enabled the service linking role for elastic load balancing. And that's just this command here. And finally we have our environment available to us to run Kubernetes.
