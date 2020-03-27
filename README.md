# Generic Rancher Cluster Playbook

Configures a Generic Rancher Cluster that is operationally ready and available to host one or more clusters depending on the underlying vm's and network capabilities. This is currently highly experimental and not recommending for a production operationally stable environment in any manner.

## Requirements
[The Amazon Command line interface is required](https://aws.amazon.com/cli/)

The following configuration:

    [profile outscale]
    output = json
    s3 =
        signature_version = s3

## Variables

    outscale_rancher_image: ami-3770adc9
    outscale_endpoint: https://fcu.us-east-2.outscale.com
    outscale_object_endpoint: https://osu.us-east-2.outscale.com
    outscale_instance_type: "tinav5.c2r4p1"
    outscale_region: us-east-2
    k8s_cluster_namespace: cloud-infrastructure
    k8s_cluster_hostname: cloudinfra
    aws_profile: outscale
    route53_profile: red #this profile should point to the aws-red account
    rancher_node_count: 3
    security_ingress: rancher-general-ingress.json

**outscale_rancher_image**: This is the outscale machine image as located in Outscale.  
**outscale_endpoint**: The Flexible Compute Unit endpoint to target  
 **outscale_object_endpoint**: The Object Storage Unit endpoint to target  
 **outscale_instance_type**: The Outscale [instance type](https://wiki.outscale.net/display/EN/Instance+Types) to target  
 **outscale_region**: The Outscale [Region](https://wiki.outscale.net/display/EN/Regions,+Endpoints+and+Availability+Zones+Reference)  
 **k8s_cluster_namespace**: The namespace for the cluster  
 **k8s_cluster_hostname**: The hostname for the cluster, the complete fqdn will be *k8s_cluster_hostname-k8s*.imedidata.net  
 **aws_profile**: The awscli profile to use for outscale  
 **route53_profile**: The awscli profile to use to access out AWS RED account  
 **rancher_node_count**: Initial node count  
 **security_ingress**: The current security ingress profile/ports for the cluster  
 
 ## Starting the cluster
 
    ansible-playbook -u outscale --private-key=/tmp/rancher_id_rsa -vvv rancher-init.yml
    
 On completion you should be able to visit k8s_cluster_hostname-k8s.imedidata.net and view your initial cluster.
