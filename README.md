# EBS Snapshot Cleanup Lambda Function

## Project Description

This project contains an AWS Lambda function designed to automatically clean up unused or orphaned EBS snapshots. Snapshots that are either not attached to any volume or are associated with volumes that are not attached to running EC2 instances are identified and deleted. This helps in reducing unnecessary storage costs and maintaining a clean AWS environment.

## Features

- **Automated Cleanup**: The function runs periodically (as per the defined schedule) to clean up unused EBS snapshots.
- **Resource Optimization**: Helps in optimizing AWS resources by deleting unnecessary EBS snapshots, thus saving storage costs.
- **Error Handling**: Gracefully handles errors, ensuring that the cleanup process is robust and reliable.

## How It Works

1. **Initialization**: The Lambda function initializes the EC2 client using the Boto3 library.
2. **Retrieve Snapshots**: It retrieves all EBS snapshots owned by the account.
3. **Retrieve Running Instances**: It retrieves all active (running) EC2 instances.
4. **Snapshot Evaluation**: For each snapshot:
   - If it is not attached to any volume, it is deleted.
   - If it is attached to a volume, the function checks whether the volume exists and whether it is attached to a running instance. If not, the snapshot is deleted.
   - If the volume associated with the snapshot is not found, the snapshot is deleted.
5. **Logging**: Actions taken by the function (such as deletion of snapshots) are logged for audit purposes.

## Usage

### Prerequisites

- AWS Account
- AWS Lambda setup
- IAM Role with the necessary permissions to execute the Lambda function (EC2 Read/Write permissions)

### Deployment

1. **Create IAM Role**: Ensure that your Lambda function has an IAM role with the following policies:
   - `AmazonEC2ReadOnlyAccess`
   - `AmazonEC2FullAccess`

2. **Lambda Function Code**: Deploy the provided Lambda function code to your AWS Lambda environment.
