# AWS Cybersecurity Threat Detection ML Pipeline

Production-style threat detection system built on AWS using SageMaker and XGBoost to identify anomalous network traffic.

## Architecture
![Architecture](architecture/secure-ml-threat-detection-architecture.png)

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
