# AWS CloudFormation Template: Auto Scaling Group, ALB, and RDS Deployment

This CloudFormation template deploys a scalable infrastructure on AWS, consisting of an Auto Scaling Group with EC2 instances, an Application Load Balancer (ALB), and an RDS database instance.

## Components
- Virtual Private Cloud (VPC): Provides a private network environment for your resources.
- Public and private Subnets
- Application Load Balancer (ALB): Distributes incoming traffic across EC2 instances and ensures high availability and scalability.
- Auto Scaling Group (ASG): Automatically scales EC2 instances based on demand.
- Amazon RDS

## Security
- Network Isolation: Public and private subnets are used to isolate different parts of the infrastructure. The ALB is placed in public subnets to handle Internet traffic, while EC2 instances and RDS are placed in private subnets to enhance security.
- Security Groups

## Reliability
- Auto Scaling: The Auto Scaling Group ensures that the number of EC2 instances scales with demand, maintaining application availability.

## Performance Efficiency
- Scalable Architecture: The use of an Auto Scaling Group and ALB ensures that the application can handle varying levels of load efficiently.
- Load Balancer: The ALB automatically distributes incoming traffic to multiple EC2 instances, improving application performance and availability.

## Cost Optimization
- On-Demand Pricing: EC2 instances are used on an on-demand basis, scaling up or down based on the application load to optimize costs.

-----------------------------------------------------------------------------------------

## CI/CD Pipeline Setup

### Pipeline Stages (AWS CodePipeline)

1. **Source Stage (AWS CodePipeline)**
   - Retrieves the CloudFormation template from Github (or any other Git repository).

2. **Build Stage (AWS CodeBuild)**
   - Uses AWS CodeBuild to validate the CloudFormation template.
   - `buildspec.yml` example:
     ```
     version: 0.2
     phases:
       build:
         commands:
           - echo "Validating CloudFormation template"
           - aws cloudformation validate-template --template-body file://template.yaml
     artifacts:
       files:
         - template.yaml
     ```

3. **Deploy Stage (AWS CloudFormation)**
   - Deploys or updates the infrastructure using AWS CloudFormation. Configured to use the validated template from CodeBuild.


### Troubleshooting

1. **Build Failures**
   - Review CodeBuild logs.
   - Validate CloudFormation template syntax.

2. **Deployment Failures**
   - Check CloudFormation stack events for errors.
   - Verify IAM permissions.

3. **Pipeline Not Triggering**
   - Verify source configuration and permissions.

4. **Health Check Failures**
   - Check EC2 instance logs for application errors.