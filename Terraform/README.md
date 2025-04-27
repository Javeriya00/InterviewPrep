# Terraform Interview Prep

This section covers Terraform-related interview questions, focusing on Infrastructure as Code (IaC) and cloud provisioning.

## Questions & Answers

### 1. What is Terraform, and how does it differ from CloudFormation?

- **Terraform** is platform-agnostic and supports multiple cloud providers like AWS, Azure, and GCP.
- **CloudFormation** is AWS-specific and deeply integrated with AWS services.

### 2. What is the role of Terraform state files?

The Terraform state file records the current state of your infrastructure. It is crucial for tracking infrastructure changes, allowing Terraform to detect and manage any differences between the real-world infrastructure and the code.

### 3. How would you handle rollbacks in Terraform?

- **Terraform** doesn’t have a direct rollback feature, but you can revert to a previous state by using a backup or versioned state file and applying the configuration again.

## Further Reading
- [Terraform Documentation](https://www.terraform.io/docs)
