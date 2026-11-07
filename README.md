# S3 Data Exfiltration Forensics

**Project Summary:**

Conducted an advanced cloud forensics investigation into an Amazon S3 data exfiltration event. Established a secure multi-layered logging pipeline by routing multi-region AWS CloudTrail S3 Data Events (GetObject/PutObject) and 1-minute aggregation VPC Flow Logs to a centralized, secured Amazon S3 evidence bucket (project3-exil-logs-718).   Simulated a threat actor by provisioning an Amazon EC2 instance (Attacker-Machine) equipped with an unauthorized IAM role (AmazonS3ReadOnlyAccess) to execute command-line data exfiltration against a sensitive victim bucket (project3-victim-data-17476). Utilizing Amazon Athena, successfully correlated control-plane API activity with underlying network transport layer logs, isolating the exact GetObject event time, source IP address, and proving a precise exfiltration volume of 74,565 bytes over HTTPS port 443.   

**Learning Points:**

1. **Multi-Tier Cloud Forensic Telemetry:** Designed and deployed a robust logging framework combining control-plane API activity (CloudTrail S3 Data Events) with network-level transport visibility (VPC Flow Logs) for complete incident reconstruction.
2. **Control-to-Transport Log Correlation:** Mastered cross-domain forensic analysis by using Amazon Athena to map high-level user activities (CloudTrail GetObject event timestamps and source IPs) down to low-level network byte counts and packet flows (vpc_flow_logs).
3. **Data Exfiltration Measurement & Quantification:** Successfully identified and isolated specific data theft metrics, utilizing Athena SQL queries to confirm an exact data payload transfer of 74,565 bytes originating from an EC2 private IP (172.31.46.166) to an external S3 public endpoint.
4. **IAM Role Misconfiguration & Privilege Abuse:** Investigated how threat actors weaponize overly permissive IAM roles (AmazonS3ReadOnlyAccess) attached to compromised or rogue EC2 compute resources to plunder sensitive storage buckets.
5. **PICERL Framework in Data Leak Scenarios:** Executed a structured incident response lifecycle focusing heavily on the "Identification" and "Lessons Learned" phases to trace data egress paths and quantify the full scope of a cloud data breach.
6. **Cloud Data Perimeter & Egress Hardening:** Established critical remediation strategies, highlighting the implementation of VPC Gateway Endpoints, strict IAM Condition Keys (aws:SourceVpc / aws:SourceIp), and automated threat detection via Amazon GuardDuty to prevent unauthorized data theft.  
