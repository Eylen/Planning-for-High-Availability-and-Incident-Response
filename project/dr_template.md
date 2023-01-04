# Infrastructure

## AWS Zones
Identify your zones here

zone 1: us-east-2
zone 1 availabilty zones:
- us-east-2a
- us-east-2b
- us-east-2c

zone 2: us-west-1
zone 2 availability zones:
- us-west-1a
- us-west-1b
## Servers and Clusters

### Table 1.1 Summary
| Asset            | Purpose                                  | Size        | Qty | DR                                               |
|------------------|------------------------------------------|-------------|-----|--------------------------------------------------|
| VPC              | Virtual Private Cloud                    | N/A         | 1   | Created in multiple locations and deployed to DR |
| EC2 (Ubuntu web) | Flask application                        | t3.micro    | 3   | Created in multiple locations and deployed to DR |
| EKS              | Kubernetes cluster                       | t3.medium   | 2   | Created in multiple locations and deployed to DR |
| ALB              | Aplication load balancer                 | N/A         | 1   | Created in multiple locations and deployed to DR |
| RDS              | Aurora                                   | db.t2.small | 2   | Replicated and created in multiple locations     |
| SSH Keys         | To access EC2 instances                  | N/A         |     | Stored in a secure place                         |
| Terraform code   | Terraform code to mantain infrastructure | N/A         |     | Stored in github or some other code repository   |


### Descriptions
More detailed descriptions of each asset identified above.

- VPC: Virtual Private cloud to secure communications 
- EC2: Elastic Compute Cloud running web application
- EKS: Elastic Kubernetess Service where monitoring will be deployed (Prometheus and Grafana)
- ALB: Application Load Balancer, distributes requests across ec2 instances
- RDS: AWS Relational Database Service using Aurora database 

## DR Plan
### Pre-Steps:
List steps you would perform to setup the infrastructure in the other region. It doesn't have to be super detailed, but high-level should suffice.

- create S3 bucket with `udacity-tf-spicado-west` name in us-west-1 if it doesn't exist
- Ensure that the infrastructure of zone1has the same infrastructure than zone1 in terraform code
- open AWS console in us-west-1 region and clone github code
- Run `terraform init` and `terraform apply` in zone2 folder
- Install and configure Prometheus and grafana for monitoring


## Steps:
You won't actually perform these steps, but write out what you would do to "fail-over" your application and database cluster to the other region. Think about all the pieces that were setup and how you would use those in the other region

- Point DNS to the secondary region
- Force secondary region to become primary at DB level
