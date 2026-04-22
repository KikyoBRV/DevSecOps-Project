# Kubernetes Multi-Cluster & Multi-Cloud E-Commerce System with Consul

## Project Overview
This repository demonstrates the deployment of a multi-cloud e-commerce system 
across two Kubernetes clusters: AWS EKS and DigitalOcean Kubernetes (DOKS). 
HashiCorp Consul is used as the Service Mesh to enable Cluster Peering, 
secure mTLS communication, and automated traffic failover between cloud providers.

## Repository Structure

- `microservices-demo/` — Source code for the 11-tier microservices e-commerce 
  application, deployed using publicly available GCP container images as per 
  assignment instructions.
- `consul-crash-course/` — Terraform configurations and Kubernetes manifests 
  used to provision clusters, install Consul via Helm, and configure 
  cross-cloud service failover.

## Architecture

| Component        | Details                                              |
|------------------|------------------------------------------------------|
| Primary Cloud    | AWS EKS — runs the full e-commerce application stack |
| Secondary Cloud  | DigitalOcean Kubernetes — runs the backup shipping service |
| Service Mesh     | HashiCorp Consul — cluster peering, mTLS, failover   |

## Deployment Steps

1. Provision AWS EKS cluster using Terraform
2. Provision DigitalOcean Kubernetes cluster via DigitalOcean Dashboard
3. Install Consul on both clusters via Helm (version 1.0.0)
4. Configure Consul Cluster Peering between `eks` and `lke` datacenters
5. Deploy the full e-commerce application to AWS EKS
6. Deploy the backup `shippingservice` to DigitalOcean Kubernetes
7. Apply `consul-mesh-gateway.yaml` on both clusters
8. Apply `exported-service.yaml` and `service-resolver.yaml` for failover routing
9. Verify failover by accessing the frontend LoadBalancer URL

## Screenshots
Evidence of the working system can be found in the `screenshots/` folder, including:
- E-commerce Web UI (Online Boutique) running on AWS EKS
- Consul Service Mesh UI showing cluster peering status
- `kubectl get pods` output from both clusters
- `kubectl get svc` output showing LoadBalancer external IPs

## Credits and Acknowledgements

- **Application Source Code:** 
  [GoogleCloudPlatform/microservices-demo](https://github.com/GoogleCloudPlatform/microservices-demo)
- **Terraform and Kubernetes Manifests:** 
  [TechWorld with Nana — consul-crash-course](https://gitlab.com/twn-youtube/consul-crash-course)