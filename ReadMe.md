# Migration Strategies: VMs to Containers

This represents the Migration Strategies stages from Vms to Containers.

---

## **Migration strategy**

---

## **Stage 1: Discovery & Assessment**

- Identify the existing applications (stateful and stateless), their dependencies, the network flows and storage needs.
- Document CI/CD pipelines and deployment processes.
- Define success metrics such as the deployments speed, reliability, cost reduction, and observability coverage.

---

## **Stage 2: Manually Containerize a Go web app to illustrate to the Developers**

- Explain the differences and relationships between Vms and Containers.
- Explain what a docker does, its installations and how to use it to build an image of the app.
- Using Go web app for illustration, explain what a Dockerfile does and write it.
- Build the docker image and run it locally.
- Use a Docker-Compose file to build multi-services images for accessibility via the web.
- Push it to a private/public registry (docker hub) manually.

---

## **Stage 3: Continuous Integration/Continuous Deployment (CI/CD) pipeline is employment with Security**

With the aid of Github Action, a CI/CD pipeline is used to automatically integrate:

- building  
- tagging  
- testing  
- scanning  

of the image before deploying to a private registry (DOCKER HUB, ECR).

Ensure that the images are scanned for vulnerabilities using **Trivy** before deployment.

---

## **Stage 4: Multi-Environment Kubernetes (AWS EKS) setup (staging and prod) using Terraform (Terragrunt)**

### **To Set Up:**

- Multi-AZ node groups for high Availability and resilience
- Nginx or AWS Load Balancer Controller for ingress to save cost by reducing the number of cloud Load Balancers used.
- Cluster Autoscaler, Horizontal Pod Autoscaler (HPA), and Vertical Pod Autoscaler (VPA) for Autoscaling
- ExternalDNS & Cert-Manager to ensure customers/clients data encryption
- **Observability:** Prometheus, Grafana and EFK to enable active and proactive understanding of the internal state of the system and detect problems fast before it escalates.
- GitOps using **ArgoCD** to ensure continuous delivery, automated deployments, improved security, easy rollbacks and self healing.

---

## **Stage 5: Kustomize for Kubernetes Manifests**

- Set up Kustomize for required Kubernetes Manifests based on multiple Environments and Namespaces.

---

## **Stage 6: Role Base Access Control (RBAC) and Pod Security and Network Policies Enforcement**

- To limit the extent of a blast Radius in case of any attack, it is important that for each workload that is set up in the kubernetes cluster, least priviledge is ensured.
- Service Account is created for each pod, with roles indicating permissions for each workloads, with the aid of a Role Binding, they are binded together.

---

## **Stage 7: Secrets Management**

- Secrets such as Api keys, JWT_SECRETS ought to be managed by a third party secret manager such as Harshicorp Vault, AWS Secret Manager etc, to prevent attackers from accessing them in the clusters.
- A Kubernetes Operator used in achieving this is **ESO (External Secret Operator)** with the aid of a custom resource definition `externalsecret` and `secretstore` YAML manifests to connect to the secret store.
