AWS Infrastructure Automation with SSM.

This repository contains the workflow and documentation for automating AWS infrastructure deployment using AWS Systems Manager (SSM) Automation.

By utilizing SSM Automation documents, I transitioned from manual EC2 configuration to a "hands-off," repeatable deployment process that handles both infrastructure provisioning and software bootstrapping.

📍 Project Overview

In this project, I leveraged the Executing Automation Workflow Using AWS SSM Automation lab to build a custom automation document. This document orchestrates the launch of an EC2 instance and automatically installs specific application stacks based on user input.

🛠️ Technical Steps Taken

Workflow Definition: Authored a JSON-based SSM Automation document to define sequential steps for AWS API calls.

Resource Provisioning: Configured the automation to launch EC2 instances with a pre-defined IAM role (MyEC2SSMRole) to ensure the SSM Agent could communicate with the service immediately.

Dynamic Bootstrapping: Implemented logic to allow the user to choose between deploying MariaDB or Apache (httpd) at runtime.

Security-Focused Validation: Used AWS Systems Manager Session Manager to access the instances securely (no SSH/Port 22 required) and verify the success of the deployment.

📂 Repository Structure

/templates: Contains the JSON Automation Document used to define the workflow.

/scripts: Validation commands and scripts for testing service health.

README.md: Project documentation and lessons learned.

🎓 Lessons Learned

IAM Instance Profiles: Reinforced the necessity of the AmazonSSMManagedInstanceCore policy; without it, the instance remains "unmanaged" by SSM regardless of the automation success.

Agent-Based Management: Learned the security benefits of using Session Manager for verification, which eliminates the need for managing .pem keys and opening inbound security group ports.

Input Parameterization: Gained experience in making automation documents flexible by using parameters (like selecting between MariaDB and Apache) to serve different environment needs.

🚀 How to Run

Import Document: Copy the JSON from the /template folder.

Create SSM Document: In the AWS Console, go to Systems Manager > Documents > Create Automation.

Execute: Choose Execute Automation, select the document, and choose your Application (e.g., mariadb-server).

Verify: Once the status shows Success, use Session Manager to log in and run:
