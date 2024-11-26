# Infrastructure

## AWS Zones
Identify your AWS zones here:
- Zone 1: US-EAST-2
- Zone 2: US-WEST-1

## Servers and Clusters

### Table 1.1: Summary
| Asset             | Purpose               | Size        | Qty   | DR                                                      |
|-------------------|-----------------------|-------------|-------|---------------------------------------------------------|
| VPC               | Virtual Network       | -           | 2     | 2 zones, 1 VPC each zone for DR purposes                 |
| EC2 instances     | Application Servers   | t3.micro    | 6     | 2 zones, 3 instances each zone for DR purposes           |
| EC2 keypair       | SSH key for access to EC2 | -         | 2     | 1 keypair each zone for EC2 instance access             |
| EKS               | Kubernetes Clusters   | t3.medium   | 4     | 2 zones, 2 nodes each zone for DR purposes               |
| Prometheus Grafana| Monitoring System     | -           | 2     | 2 zones, 2 nodes each zone for DR purposes               |
| S3 bucket         | Bucket for Terraform  | -           | 2     | 2 zones, 1 bucket each zone for DR purposes              |
| ALB               | Application Load Balancer | -        | 2     | For High Availability (HA) and DR purposes              |
| RDS               | Backend Database      | db.t3.micro | 2     | 1 cluster with 2 nodes in Zone 1                        |
| RDS               | Backend Database      | db.t3.micro | 2     | 1 replicated cluster with 2 nodes in Zone 2 (replicated from Zone 1) |

### Descriptions:
- VPC: Virtual Private Cloud (VPC) - networking for the cloud infra.
- EC2 instances: VMs those running the application.
- EC2 keypair: SSH key for secure access to EC2.
- EKS: Kubernetes clusters for deploying Prometheus and Grafana.
- Prometheus Grafana: Monitoring stack.
- S3 bucket: Store Terraform state files.
- ALB: Application Load Balancer used for distributing traffic.
- RDS: Relational Database Service (RDS) clusters for storing application data.

## DR Plan

### Pre-Steps:
- Ensure that the disaster recovery (DR) site is correctly set up and working normally.

### Steps:
1. Database: Promote the replicated RDS cluster at the DR site.
2. Traffic: Reroute traffic to the DR site.
