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



# Creating IAM roles and policies
- [Instructor] In order to implement our EKS environment we first have to be able to provide the right level of credentials to the different users that we might create. In order to do that, we've got a document here in our module directory. Do an ls, we get I-AM_Polices, so we'll do a more on our I-A-M Policies Roles file. We're going to give EKS cluster services access to users of the EKS environment and we also are going to use cloud formation to deploy the environment, and eventually also to potentially read into the environment. So our administrator, the resource that we are going to give administrative access is going to need administrative access. But we also need to create this EKS Policy for EKS specific users. I'm going to grab this, we're going to this policy first, and then we'll create another policy which is basically a cloud formation policy. And really this is an administrative full admin access policy for the cloud formation resource. And we'll associate that with a user that we'll create for cluster administrator equivalent role. 

### In general, you'd use cluster users that would have EKS access for EKS services and an administrator to actually create resources. And so that's the way it differentiates those two roles.

We also need a role for EKS, and this so that EKS itself can programmatically do things against your account. And so we are going to create that role and that role will get passed into the system as well. So with the policies let's go and jump and create those first. So we're going to create our policy. We're going to use the JSON form so we can paste in our JSON object that we captured from the document. Click on review. Give it our name: AdminEKSPolicy. And so create that policy. Okay. And we need to create a second policy though, so it's actually the right spot to be. Go back to JSON, we'll scroll down here and grab this one. Our cloud formation policy is really the administrator policy, so realize this is giving full access to the user that will get this policy. But it is needed in order to implement the cloud formation processes. 


It's also useful for allowing that user, the user that owns the environment and it's interesting that the user creates the EKS environment really is the underlying owner of all of this, in order to get access to some of the additional metering, or rather metrics type capabilities, this user does need most of these credentials. We're going to give this policy a name: AdminCloudFormationPolicy. So obviously you don't want to use this user as a regular user that's going to become a cluster admin level user. So great, we've created our policies the other thing that we need to is create a role. And the role we're going to create is a known role with an EKS environment. So, I'm just selecting here an AWS service based role. Choose the service that you'll use, and if we scroll down EKS is here in the list and that's what we need. So we just want to make sure we have the cluster in the service policy and we're going to call this, how about ClusterEksRole. And the last that thing we need to do is we need to actually grab the role ARN, we're going to need this later. 


So the role ARN is just the path to the Amazon overall resource and so we can just copy that by clicking the little double icon here or we could also select it, then copy it as well. We're going to jump back into our terminal and here what we're going to do is we're going to actually store this and I have a file that I created a directory up from all the modules called output.txt. And that's just for us to capture the data. So we're going to edit that file V-I ../output.txt. And I'm going to do capital M using V-I, so capital A puts me at the end of the line, cmd V to paste that, and so now I've captured the role. And again, we're going to reuse that when we actually go to manually create the EKS cluster with the command line.
