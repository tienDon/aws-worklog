---
title: "Blog 1"
date: 2025-12-09
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Modernizing your application isn't difficult: Migrating to Amazon EKS with your existing NLB configuration

**Authors:**

- Henrique Santana, Container Specialist, AWS

- Luis Felipe, Core Solution Architect, AWS

_Date: March 25, 2025_

<style>
body {
font-family: "Times New Roman", Times, serif;

font-size: 13px;

}

h1 {
font-size: 24px;

}

h2 {
font-size: 18px;

}

h3 {
font-size: 16px;

}

</style>

## Introduction

Many organizations have built their infrastructure using [Amazon Elastic Compute Cloud (Amazon EC2)](https://aws.amazon.com/ec2/) and [Network Load Balancer (NLB)](https://aws.amazon.com/elasticloadbalancing/network-load-balancer/), often with security policies built around the NLB's static IP address. When these organizations adopt containerization and switch to [Amazon Elastic Kubernetes Service (Amazon EKS)](https://aws.amazon.com/eks/) for their modern applications, they face a significant challenge in maintaining their existing endpoint configuration. This can make modernization complicated and risky, as changes to load balancing configurations can disrupt client connectivity or require major DNS changes.

The good news is that this transition doesn't necessarily have to be an all-or-nothing effort. In this post, we explore a [hybrid deployment pattern](https://aws.amazon.com/blogs/containers/patterns-for-targetgroupbinding-with-aws-load-balancer-controller/) that provides a smooth, low-risk migration path from Amazon EC2 to Amazon EKS.

## Hybrid Deployment

Similar to the [blue/green deployment pattern](https://docs.aws.amazon.com/whitepapers/latest/overview-deployment-options/bluegreen-deployments.html), our hybrid deployment approach supports running the application concurrently on Amazon EKS and Amazon EC2 during the migration. The key to this strategy is the ability to route traffic through your existing load balancer to both deployments using TargetGroupBinding, resulting in a controlled migration process.

### Architecture

![Figure 1: Traffic flow diagram showing migration from Amazon EC2 (green) to Amazon EKS (blue)](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2025/03/18/Picture1-8.png)

_Figure 1: Traffic flow diagram showing migration from Amazon EC2 (green) to Amazon EKS (blue)_

## Advantages of using a hybrid deployment approach {: style="font-size: 18px;"}

The hybrid deployment approach offers the following advantages:

• **Controlled migration:** Gradually route traffic to the EKS workload while maintaining service through the existing EC2 infrastructure With your own approach, significantly reduce migration risk.

• **Simple Rollback:** Quickly redirect traffic back to EC2 instances if issues arise, providing reliable rollback during migration.

• **A/B Testing:** Compare performance between EC2 and EKS deployments under real-world conditions, providing data-driven decisions on the most efficient configuration and resource allocation.

• **Flexibility:** Leverage the strengths of both deployment environments during the migration, optimizing workload placement based on specific requirements.

• **Minimized Service Interruption:** Reduce downtime risk by running both environments concurrently during migration.

• **Risk Reduction:** Validate containerized deployments with real traffic while maintaining fallback options, providing business continuity.

## Prerequisites for Migration

This post is written assuming you have a basic understanding of Docker containerization and Kubernetes concepts (pods, events, namespaces, and deployments, etc.).

Before beginning the migration process, ensure you have the following components available:

• **Existing Infrastructure:** In our example, a [Retail Store sample application](https://github.com/aws-containers/retail-store-sample-app) is running on Amazon EC2.

• **Container Requirements:** A tested and containerized application, with the container image pushed to the container registry, such as [Amazon Elastic Container Registry (Amazon ECR)](https://aws.amazon.com/ecr/).

• **Amazon EKS Environment:** [EKS cluster with supported Kubernetes version](https://docs.aws.amazon.com/eks/latest/userguide/kubernetes-versions.html#available-versions) across multiple [Availability Zones (AZs)](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/).

• **Tools:**
◦ [kubectl](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html) has been installed and configured to interact with the Amazon EKS cluster.

◦ [AWS Command Line Interface (AWS CLI)](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) has been installed and configured with the appropriate [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/).
◦ [AWS Load Balancer Controller](https://docs.aws.amazon.com/eks/latest/userguide/lbc-helm.html) has been installed on the Amazon EKS cluster.

## Migrate your application using a hybrid deployment with NLB {: style="font-size: 18px;"}

### Detailed migration steps {: style="font-size: 16px;"}

The first step is to create a new target group:

```bash
TARGET_GROUP_ARN=$(aws elbv2 create-target-group \

--name eks-green \

--protocol TCP \

--port 80 \

--target-type ip \

--vpc-id <VPCID> \

--query 'TargetGroups[0].TargetGroupArn' \

--output text)
```

The ARN (Amazon Resource Name) of the target group is stored in the TARGET_GROUP_ARN variable. Next, verify that both target groups (Amazon EC2 and Amazon EKS) are configured with `Terminate connections on deregistration` set to true.

```bash
aws elbv2 describe-target-group-attributes \

--target-group-arn $TARGET_GROUP_ARN \

--query 'Attributes[*]' --output text | \

grep deregistration_delay.connection_termination.enabled
```

Observe the following output:

`deregistration_delay.connection_termination.enabled true`

If the command output returns `false`, it means this feature is not enabled. To enable it, use the following command:

```bash
aws elbv2 modify-target-group-attributes \

--target-group-arn $TARGET_GROUP_ARN \

--attributes 'Key=deregistration_delay.connection_termination.enabled,Value=true' \

--query 'Attributes[*]' --output text | \

grep deregistration_delay.connection_termination.enabled
```

At this stage, traffic is still directed to the application running on Amazon EC2. Now you can deploy the containerized application on the Amazon EKS cluster:

```bash
kubectl create deployment myapp \

--image public.ecr.aws/aws-containers/retail-store-sample-ui:0.8.1 \

--replicas 2 --port=8080
```

We can expose the application by creating a service. This is the YAML file for the service:

```yaml
cat << EOF > service.yaml
apiVersion: v1
kind: Service
metadata:

labels:
app: myapp
name: ui-service
namespace: default
spec:
ports:

- port: 80
targetPort: 8080
selector:

app: myapp
type: ClusterIP
EOF
```

We can apply it:

```bash
kubectl apply -f service.yaml
```

With the application running and exposed as a Kubernetes service, create a new listener for the existing NLB:

```bash
aws elbv2 create-listener \

--load-balancer-arn <NLB-ARN> \

--protocol TCP --port 81 \

--default-actions Type=forward,TargetGroupArn=$TARGET_GROUP_ARN
```

Currently, you have a listener on port 80. This listener continues to forward traffic to the target group associated with EC2 instances. The newly created listener forwards traffic to the target group associated with Amazon EKS. It doesn't have any target until you use TargetGroupBinding to bind the service to the new target group. We can create it:

```yaml
cat << EOF > tg-binding.yaml
apiVersion: elbv2.k8s.aws/v1beta1
kind: TargetGroupBinding
metadata:

name: ui-tgbinding
spec:

serviceRef:

name: ui-service # Service name
port: 80 # Service port
targetGroupARN: $TARGET_GROUP_ARN
EOF
```

Apply manifest:

```bash
kubectl apply -f tg-binding.yaml
```

You can verify that the targets are properly registered to the Amazon EKS target group. Give the targets enough time to pass the health check, then verify that the new targets can successfully serve traffic. If the health check fails, verify that the Amazon EKS node's Security Group allows the necessary traffic. To confirm proper functionality, try accessing the application through the new listener to ensure it's being served as intended before proceeding with the addition.

Before starting the migration, you need to create another listener pointing to the existing EC2 target group:

```bash
aws elbv2 create-listener \

--load-balancer-arn <NLB-ARN> \

--protocol TCP --port 82 \

--default-actions Type=forward,TargetGroupArn=<EC2-TARGET-GROUP-ARN>
```

After this step, NLB has three listeners (ports 80, 81, and 82), where you've created two more listeners to perform the smooth traffic migration. The port numbers used in this post are examples, and you can choose port numbers to reflect your application's needs. We recommend checking if traffic to existing target groups is being served on the new listener. This ensures that the NLB configuration is ready to proceed with the next steps.

### Moving traffic from Amazon EC2 to Amazon EKS target group {: style="font-size: 16px;"}

Both target groups are healthy, and all listeners are ready to handle traffic, so it's time to move the traffic. First, configure the existing listener on port 80 to send traffic to the `eks-green` target group:

```bash
aws elbv2 modify-listener \

--listener-arn <NLB-Listen-80> \

--default-actions Type=forward,TargetGroupArn=$TARGET_GROUP_ARN
```

Changing this configuration ensures that all new flows are redirected to the new target group. Because the targets passed their health check when linked to the listener on port 81, this helps
This will speed up the process.

This listener change may take a few minutes to propagate. Therefore, we recommend monitoring traffic going to targets in the new target group before proceeding with the next steps. During this time, it's important to monitor your application's behavior and performance metrics. You can monitor the target's health status using:

```bash
aws elbv2 describe-target-health \

--target-group-arn $TARGET_GROUP_ARN
```

While existing connections will not be affected, new connections will stop routing to the old target group after the traffic migration is complete. After confirming that the new targets are successfully handling traffic and that the previously existing targets are no longer serving traffic, retrieve a list of targets from the previously existing EC2 target group to prepare for deregistration:

```bash
aws elbv2 describe-target-health \

--target-group-arn <EC2-TARGET-GROUP-ARN> \

--query 'TargetHealthDescriptions[*].Target.Id' \

--output text
```

This command outputs a list of instance IDs. For each instance ID, run the `deregister-targets` command:

```bash
aws elbv2 deregister-targets \

--target-group-arn <EC2-TARGET-GROUP-ARN> \

--targets Id=<InstanceID>
```

The deregistration step is crucial because the EC2 target group remains associated with NLB via the port 82 listener. When executed, the deregister-targets call performs a `Connection termination on deregistration`, which terminates existing connections to the old targets. When clients reconnect, they are routed to the targets of the new Amazon EKS target group.

### Rollback to Original Target Group Procedure (If Needed) {: style="font-size: 16px;"}

If you need to roll back to the original EC2 target group, follow these steps:

1. Re-register all original targets to the EC2 target group:

```bash
aws elbv2 register-targets \

--target-group-arn <EC2-TARGET-GROUP-ARN> \

--targets Id=<InstanceID1> Id=<InstanceID2>
```

2. Wait for the targets to pass the health check. Monitor their health status:

```bash
aws elbv2 describe-target-health \

--target-group-arn <EC2-TARGET-GROUP-ARN>
```

3. Reconfigure the listener on port 80 on NLB to send traffic to the target group EC2:

```bash
aws elbv2 modify-listener \

--listener-arn <NLB-Listen-80> \

--default-actions Type=forward,TargetGroupArn=<EC2-TARGET-GROUP-ARN>
```

### Cleanup after migration {: style="font-size: 16px;"}

If the migration was successful (no rollback needed), then you can proceed with cleanup operations. This includes deleting the two additional listeners you created on ports 81 and 82, as they were only necessary for the migration process. Finally, you can safely delete the EC2 target group, as it no longer receives any traffic.

```bash
aws elbv2 delete-listener \

--listener-arn <Listen-Port81-ARN>

aws elbv2 delete-listener \

--listener-arn <Listen-Port82-ARN>

aws elbv2 delete-target-group \

--target-group-arn <EC2-TG-ARN>
```

## Conclusion

The hybrid deployment pattern using NLB and TargetGroupBinding provides a practical, low-risk approach to migrating applications to Amazon EKS from various sources, including Amazon EC2, on-premises infrastructure, or other container orchestration solutions. Maintaining the existing NLB configuration while gradually transitioning traffic to containerized workloads allows this approach to support a smooth transition and provide integrated rollback capabilities. While we focused on migrating from Amazon EC2 to Amazon EKS, the flexibility of this pattern extends to many different scenarios, including transitions from on-premises infrastructure or other container orchestration solutions.

Recent improvements to the AWS Load Balancer Controller, particularly the introduction of the [target group MultiCluster](https://kubernetes-sigs.github.io/aws-load-balancer-controller/latest/guide/use_cases/multi_cluster/), further expand these capabilities. Organizations can now manage workloads across multiple Kubernetes clusters and integrate with non-cluster resources, facilitating more complex migration strategies and distributed application architectures. This hybrid approach serves as a reliable blueprint for modernization, providing the necessary tools to maintain business continuity and mitigate risk while offering the flexibility to adapt to evolving infrastructure requirements.

To continue your migration journey, we recommend reading our companion post: [Migrating from Self-Managed Kubernetes to Amazon EKS: Here Are Some Key Considerations](https://aws.amazon.com/blogs/containers/migrating-from-self-managed-kubernetes-to-amazon-eks-here-are-some-key-considerations/). This post provides further insights and best practices that complement the hybrid deployment strategy discussed here, especially if you are migrating from a self-managed Kubernetes environment to Amazon EKS.

**TAGS**: [EKS](https://aws.amazon.com/blogs/containers/tag/eks/), [elb](https://aws.amazon.com/blogs/containers/tag/elb/), [nlb](https://aws.amazon.com/blogs/containers/tag/nlb/)
