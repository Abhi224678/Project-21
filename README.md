
# Project 21: CloudWatch Monitoring Dashboard

## 1. Overview

The objective of this project is to monitor and visualize the performance of Amazon EC2 instances using an AWS CloudWatch Dashboard.

Created a custom CloudWatch dashboard containing multiple monitoring widgets to track CPU utilization, network traffic, and EC2 status checks for two EC2 instances.

The dashboard provides a centralized view of infrastructure performance and helps identify potential performance issues.

## 2. AWS Services and Technologies Used

- Amazon CloudWatch
- Amazon EC2
- AWS CLI
- AWS Management Console
- JSON

## 3. EC2 Instances Monitored

Used the two EC2 instances deployed in Project 20 for monitoring.

| Configuration | EC2 Instance 1 | EC2 Instance 2 |
|---|---|---|
| Instance Name | project20-web-1 | project20-web-2 |
| Instance ID | i-07d0c03dfc9a28017 | i-037a278fbb6f24c77 |
| Private IP | 172.31.200.73 | 172.31.76.105 |
| Availability Zone | ap-south-1a | ap-south-1b |
| Instance Type | t2.micro | t2.micro |
| State | Running | Running |

## 4. Implementation Steps

### Step 1: Verified EC2 Instances

Verified that both EC2 instances were running using the AWS CLI.

Command used:

```bash
aws ec2 describe-instances \
  --instance-ids i-07d0c03dfc9a28017 i-037a278fbb6f24c77 \
  --region ap-south-1
```

Both instances were successfully verified in the running state.

### Step 2: Created Dashboard Configuration

Created a JSON configuration file named `dashboard.json`.

The configuration defines four CloudWatch metric widgets.

### Step 3: Configured CloudWatch Monitoring Widgets

Added the following four widgets to the dashboard:

| Widget | Metric | Description |
|---|---|---|
| Widget 1 | CPUUtilization | Monitors CPU utilization of EC2 Instance 1 |
| Widget 2 | CPUUtilization | Monitors CPU utilization of EC2 Instance 2 |
| Widget 3 | NetworkIn and NetworkOut | Monitors network traffic for both instances |
| Widget 4 | StatusCheckFailed | Monitors EC2 status check failures |

All metrics use the AWS/EC2 namespace.

### Step 4: Configured Metric Properties

Configured the dashboard widgets with the following settings:

| Configuration | Value |
|---|---|
| AWS Region | ap-south-1 |
| Metric Namespace | AWS/EC2 |
| Monitoring Period | 300 seconds |
| CPU Statistic | Average |
| Network Statistic | Sum |
| Status Check Statistic | Maximum |
| Dashboard Type | Time Series |

### Step 5: Validated Dashboard JSON

Validated the JSON configuration before uploading it to CloudWatch.

Command used:

```bash
python3 -m json.tool dashboard.json
```

The JSON configuration was successfully validated without errors.

### Step 6: Created CloudWatch Dashboard

Created the CloudWatch dashboard using the AWS CLI.

Command used:

```bash
aws cloudwatch put-dashboard \
  --dashboard-name Abhijeet-Project21-Dashboard \
  --dashboard-body file://dashboard.json \
  --region ap-south-1
```

The dashboard was successfully created.

Validation response:

```json
{
    "DashboardValidationMessages": []
}
```

### Step 7: Verified Dashboard Creation

Verified the dashboard using the following command:

```bash
aws cloudwatch list-dashboards \
  --region ap-south-1 \
  --query "DashboardEntries[?DashboardName=='Abhijeet-Project21-Dashboard']" \
  --output table
```

The dashboard appeared successfully in the CloudWatch dashboard list.

## 5. Dashboard Details

| Configuration | Value |
|---|---|
| Dashboard Name | Abhijeet-Project21-Dashboard |
| AWS Account | 590507089733 |
| AWS Region | ap-south-1 |
| Number of Widgets | 4 |
| Dashboard Status | Successfully Created |

## 6. Screenshots and Evidence

Add the following screenshot as evidence of successful implementation:

| Screenshot | Description |
|---|---|
| P21-01-CloudWatch-Dashboard.png | CloudWatch dashboard displaying the four monitoring widgets |

## 7. Project Outcome

Successfully created an AWS CloudWatch monitoring dashboard for two EC2 instances.

The following objectives were achieved:

- Created a custom CloudWatch dashboard.
- Configured CPU utilization monitoring for both EC2 instances.
- Added network traffic monitoring using NetworkIn and NetworkOut metrics.
- Configured EC2 status check monitoring.
- Validated the dashboard JSON configuration.
- Successfully deployed and verified the dashboard using AWS CLI.
- Centralized EC2 performance monitoring in one dashboard.

## 8. Conclusion

This project demonstrates how Amazon CloudWatch can be used to monitor and visualize EC2 infrastructure performance through a centralized dashboard.

The dashboard provides visibility into CPU utilization, network traffic, and instance status checks, helping administrators monitor infrastructure health and identify potential performance issues.

**Project Status: Completed**
