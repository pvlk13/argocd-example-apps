# ArgoCD in Multi Cluster Environment

ArgoCD is a GipOps based tool and its very popular in CD space. Traditionally the CD part is managed by scripts , python or ansible but they come with lot of drawbacks and which are addressed by ArgoCD.

GitOps uses GIT as a single source of source of truth to deliver applications and infrastructure 

If your source code has a mechanism  of tracking  then why can’t your deployment have the mechanism of tracking which triggered the idea of this GitOps . If CI has a Git integrated  approach  then why can’t the CD have?

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%201.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%202.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%203.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%204.png)

ApI server is a CLI tool for the user to connect to ArgoCD and Dex is used for SSO for authentication purposes. Redis is used for cache your application.

Installation :

ArgoCD can be installed using :

YAML manifest

Helm

Operator

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%205.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%206.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%207.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%208.png)

Now to access the UI of argoCD from browser we need to do port forwarding 

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%209.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2010.png)

username is admin for password 

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2011.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2012.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2013.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2014.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2015.png)

==================================================

ArgoCD comes 2 modes of deployment :

hubspoke model     & standalone model 

In standalone model each argoCD is responsible for managing a single cluster .

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2016.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2017.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2018.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2019.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2020.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2021.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2022.png)

Setting up IAM permissions without this its hard for communication between the clusters . As ArgoCD will be installed it needs these permissions.

for spoke-cluster-2

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2023.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2024.png)

for spoke-cluster-1

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2025.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2026.png)

for hub-cluster

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2027.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2028.png)

Install ArgoCD in hub-cluster 

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2029.png)

t3.small was too small so there was problem with IP allocation so I had to upscale it 

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2030.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2031.png)

Now we will login into ArgoCD using HTTP mode

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2032.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2033.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2034.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2035.png)

Change the server to run as NodePort 

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2036.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2037.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2038.png)

Now the port is mapped to the Nodeport of your cluster what it means is that you can access the application from any of this hub EC2 instances IP address 

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2039.png)

Allow the port 80 in the inbound 

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2040.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2041.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2042.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2043.png)

by default they are base 64 encoded so decode it

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2044.png)

ArgoCD UI doesn’t allow you to add Cluster you can delete it but can’t add so we need ArgoCD CLI

Go to [https://argo-cd.readthedocs.io/en/stable/cli_installation/](https://argo-cd.readthedocs.io/en/stable/cli_installation/)
from here based on your OS install the argo-cd 

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2045.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2046.png)

Now need to add the clusters to your argoCD so for that first login into argoCD using argo-cd cli. 

[https://www.notion.so](https://www.notion.so)

 

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2047.png)

To add the cluster to the argocd 
   argocd cluster add [vijaya13@spoke-cluster-1.us-east-1.eksctl.io](mailto:vijaya13@spoke-cluster-1.us-east-1.eksctl.io) --server 44.206.229.150:30634

argued cluster add  spoke-cluster-1  — server (ip from argocd )

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2048.png)

Same way add the spoke-cluster-2 —server (ip from argocd)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2049.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2050.png)

you can clone any git to point in your spoke cluster I am using the example from argocd 
[https://github.com/argoproj/argocd-example-apps/tree/master/guestbook](https://github.com/argoproj/argocd-example-apps/tree/master/guestbook)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2051.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2052.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2053.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2054.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2055.png)

Likewise create for another cluster URL also 

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2056.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2057.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2058.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2059.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2060.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2061.png)

To check the working of ArgoCD change the history limits from 3 to 4 . 

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2062.png)

you can see the same getting reflected in the deployed application in Kubernetes cluster

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2063.png)

Now let us check the reverser process too where the limit changed from 4 to 3

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2064.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2065.png)

This is correct because in ArgoCD there is single source of truth that it Git(in this case) so what is in Git is taken as truth so the reverse will not work and it doesn’t allow to change your git code.

So in this case sync by checking in prune (then it discards what ever u committed which is not present in git and redeploys ) in the cluster you see now 

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2066.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2067.png)

Now delete all the clusters 

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2068.png)

similarly delete other two simultaneously which saves time than deleting each individually.

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2069.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2070.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2071.png)

check even in cloud formations if everything  is deleted

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2072.png)

![image.png](ArgoCD%20in%20Multi%20Cluster%20Environment/image%2073.png)