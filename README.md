# AWS Security Alerting System

## Overview
This project demonstrates how to set up a cloud-native security alerting system using AWS services such as GuardDuty, CloudWatch, and SNS. It detects potential security threats and sends notifications to ensure swift mitigation of security incidents.

## Features
- **Threat Detection**: Real-time identification of security threats using AWS GuardDuty.
- **Alerting and Monitoring**: Configured CloudWatch rules to trigger notifications for GuardDuty findings based on severity levels.
- **Notification System**: Integrated SNS for real-time email notifications.

## Architecture Diagram
![Architecture Diagram](path/to/architecture-diagram.png)

## Technologies Used
- AWS GuardDuty
- AWS CloudWatch (Event Rules, Metrics, Logs)
- AWS SNS

## Setup Instructions

### Prerequisites
- An AWS account with permissions to access GuardDuty, CloudWatch, and SNS.
- Basic knowledge of AWS services and configurations.

### Step 1: Enable GuardDuty
1. Navigate to the AWS Management Console.
2. Go to **GuardDuty** and enable the service.
3. Optionally, enable GuardDuty for multiple regions and accounts for comprehensive monitoring.

### Step 2: Configure CloudWatch Rule
1. Navigate to **CloudWatch** > **Rules**.
2. Create a new rule with the following settings:
   - **Event Source**: Select `GuardDuty` as the event source.
   - **Event Pattern**:
     ```json
     {
       "source": ["aws.guardduty"],
       "detail-type": ["GuardDuty Finding"],
       "detail": {
         "severity": [{ "numeric": [">=", 8] }]
       }
     }
     ```
   - **Target**: Choose `SNS Topic` for alerting.

### Step 3: Configure SNS for Notifications
1. Navigate to **SNS** > **Topics**.
2. Create a new topic (e.g., `guardduty-alerts`).
3. Add an email subscription to the topic and confirm the subscription via the email link.

### Step 4: Test the System
1. Use the AWS CLI to generate sample GuardDuty findings:
   ```bash
   aws guardduty create-sample-findings --detector-id <detector-id>
   ```
2. Verify that:
   - Findings appear in GuardDuty.
   - CloudWatch triggers the rule.
   - Notifications are sent via SNS.

## Demo
### Screenshots
- **GuardDuty Findings**:
  ![GuardDuty Findings](path/to/guardduty-findings.png)
- **CloudWatch Rule Configuration**:
  ![CloudWatch Rule](path/to/cloudwatch-rule.png)
- **SNS Email Notification**:
  ![SNS Notification](path/to/sns-notification.png)



## Usage
This system can be used by organizations to:
- Monitor and respond to security threats in AWS environments.
- Ensure compliance with security best practices.

## Future Enhancements
- **Integration with AWS Security Hub**: Centralize findings from multiple AWS services.
- **Log Aggregation**: Store findings in S3 or a third-party SIEM for long-term analysis.
- **Multi-Account Monitoring**: Extend the solution to monitor multiple AWS accounts.
- **Dashboard Creation**: Build a custom dashboard for monitoring security findings.

## Contact
For questions or suggestions, please reach out via [your email or GitHub profile link].
