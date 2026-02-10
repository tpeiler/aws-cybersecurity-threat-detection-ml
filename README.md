# AWS Cybersecurity Threat Detection ML Pipeline

Production-style threat detection system built on AWS using SageMaker and XGBoost to identify anomalous network traffic.

## Architecture
![Architecture](architecture/secure-ml-threat-detection-architecture.png)

## Architecture Walkthrough

This pipeline ingests network traffic logs and processes them through a secure, production-style machine learning workflow designed for threat detection.

1. **Log Ingestion**  
   Network traffic logs are uploaded to an encrypted Amazon S3 bucket.

2. **Feature Engineering**  
   An AWS Lambda function is triggered on object creation to preprocess the data and generate ML-ready features.

3. **Secure Data Storage**  
   Processed datasets are written to a versioned S3 bucket to preserve integrity and support reproducibility.

4. **Model Training**  
   Amazon SageMaker trains an XGBoost model within a private VPC using least-privilege IAM roles.

5. **Artifact Protection**  
   Trained model artifacts are stored in an encrypted S3 bucket with controlled access.

6. **Real-Time Inference**  
   The model is deployed to a SageMaker endpoint for live threat detection.

7. **Monitoring & Visibility**  
   Logs and metrics stream into Amazon CloudWatch, enabling operational monitoring and anomaly detection.

---

### Security Boundary

Critical compute resources are deployed inside a private VPC to prevent unintended public exposure.  

Security controls — including IAM, encryption, temporary credentials, and centralized logging — are enforced across every stage of the ML lifecycle.

## Threat Model

This system was designed with a security-first mindset, treating the ML pipeline as a production workload rather than a research demo. The following threat scenarios were considered during design.

### Potential Threats
- Unauthorized access to training data stored in Amazon S3
- Model poisoning through tampered datasets or preprocessing logic
- Privilege escalation due to overly permissive IAM roles
- Data exfiltration from model artifacts or inference endpoints
- Endpoint abuse through unrestricted or public access

### Mitigations Implemented
- Least-privilege IAM execution roles scoped to specific services and actions
- S3 encryption at rest (SSE-S3) for raw data, processed datasets, and model artifacts
- Versioned S3 buckets to support data integrity and rollback
- Private VPC deployment for Lambda, SageMaker training jobs, and inference endpoints
- Temporary credentials via AWS STS to avoid long-lived secrets
- Centralized logging and metrics in Amazon CloudWatch for visibility and anomaly detection

This threat model directly informed architectural decisions to ensure confidentiality, integrity, and availability across the entire machine learning lifecycle.

## Security Design Decisions

This system was designed using a security-first approach:

• All data encrypted at rest (S3 SSE)  
• IAM roles enforce least privilege  
• Temporary credentials used via STS  
• Model artifacts encrypted and versioned  
• CloudWatch enabled for detection visibility  

## Threat Model

Potential risks considered:

- Unauthorized dataset access  
- Model poisoning  
- Privilege escalation  
- Data exfiltration  
- Endpoint abuse  

Mitigations were intentionally built into the architecture.

## Why This Project Matters

Most ML demos ignore security.

This project treats ML like a production workload — where logging, IAM, encryption, and monitoring are mandatory.

## Tech Stack

AWS  
SageMaker  
Lambda  
S3  
IAM  
CloudWatch  
XGBoost  
Python  

## Future Improvements

- Add automated anomaly alerting  
- Integrate GuardDuty findings  
- Implement VPC endpoints  
- Add CI/CD security scanning  
