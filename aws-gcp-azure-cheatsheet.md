# AWS vs Azure vs GCP Cheat Sheet  

| **Category** | **AWS** | **Azure** | **GCP** |
|--------------|---------|-----------|---------|
| **Compute (VMs)** | EC2 | Virtual Machines | Compute Engine |
| **Autoscaling** | Auto Scaling Groups | Virtual Machine Scale Sets | Managed Instance Groups |
| **Containers (Managed)** | ECS / EKS (Kubernetes) | AKS (Azure Kubernetes Service) | GKE (Google Kubernetes Engine) |
| **Serverless** | Lambda | Azure Functions | Cloud Functions |
| **PaaS App Hosting** | Elastic Beanstalk | App Service | App Engine |
| **Networking (VPC)** | VPC | Virtual Network (VNet) | VPC Network |
| **Transit / Hub Routing** | Transit Gateway | **Virtual WAN** | Network Connectivity Center |
| **Load Balancer (L4)** | NLB | Azure Load Balancer | TCP/UDP Load Balancer |
| **Load Balancer (L7)** | ALB | Application Gateway | HTTP(S) Load Balancer |
| **DNS** | Route 53 | Azure DNS | Cloud DNS |
| **Content Delivery (CDN)** | CloudFront | Azure CDN | Cloud CDN |
| **Hybrid Connectivity (Private Link)** | PrivateLink | Private Link / Service Endpoint | Private Service Connect |
| **VPN** | VPN Gateway | VPN Gateway | Cloud VPN |
| **Dedicated Network** | Direct Connect | ExpressRoute | Dedicated Interconnect / Partner Interconnect |
| **Storage (Objects)** | S3 | Blob Storage | Cloud Storage |
| **Block Storage** | EBS | Managed Disks | Persistent Disks |
| **File Storage** | EFS | Azure Files | Filestore |
| **Archival Storage** | S3 Glacier | Azure Archive Storage | Cloud Storage Nearline/Coldline/Archive |
| **Database (RDBMS managed)** | RDS | Azure SQL Database | Cloud SQL |
| **NoSQL (Key-Value)** | DynamoDB | Cosmos DB | Firestore / Cloud Bigtable |
| **Data Warehouse** | Redshift | Synapse Analytics | BigQuery |
| **Caching** | ElastiCache (Redis/Memcached) | Azure Cache for Redis | Memorystore |
| **Queue & Messaging** | SQS | Azure Service Bus / Storage Queue | Pub/Sub |
| **Event Streaming** | Kinesis | Event Hubs | Pub/Sub |
| **Monitoring / Logging** | CloudWatch | Monitor + Log Analytics | Cloud Monitoring + Cloud Logging (Stackdriver) |
| **Secrets Manager** | Secrets Manager / Parameter Store | Key Vault | Secret Manager |
| **IAM** | IAM | Azure Active Directory (Entra ID) | Cloud IAM |
| **Key Management (KMS)** | KMS | Key Vault (Keys) | Cloud KMS |
| **DevOps CI/CD** | CodePipeline / CodeBuild | Azure DevOps / GitHub Actions | Cloud Build |
| **AI/ML Platform** | SageMaker | Azure ML | Vertex AI |
| **Data Lake** | S3 + Lake Formation | Data Lake Storage Gen2 | BigLake |
| **Analytics (ETL)** | Glue | Data Factory | Dataflow |
| **Stream Processing** | Kinesis Data Analytics | Stream Analytics | Dataflow / Pub/Sub |
| **Big Data Processing** | EMR | HDInsight / Synapse Spark | Dataproc |
| **Backup/Recovery** | AWS Backup | Azure Backup | Backup and DR Service |
| **Cost Management** | Cost Explorer | Cost Management + Billing | Billing + Cost Management |

---

âš¡ **Key Takeaways**:  
- **AWS Transit Gateway = Azure Virtual WAN = GCP Network Connectivity Center**  
- **AWS Lambda = Azure Functions = Google Cloud Functions**  
- **AWS RDS = Azure SQL = Cloud SQL**  