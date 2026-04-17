# PortfolioPulse – AWS Static Website CI/CD
A production-style cloud project where I built and deployed my personal portfolio website using AWS Static Website Hosting and automated the deployment workflow with CI/CD.
This project demonstrates hands-on experience with AWS core services, deployment automation, monitoring, and real-world DevOps fundamentals.

## Project Overview
The goal of this project was to host a static portfolio website on AWS and automatically deploy every new update whenever changes are pushed to GitHub.
Instead of manually uploading files every time, the deployment process is fully automated using AWS CodePipeline integrated with GitHub.

## Key Features
- Hosted a static portfolio website using Amazon S3
- Configured custom index and error pages
- Enabled public website access using bucket policies
- Automated deployments from GitHub to AWS
- Continuous delivery on every push to `main`
- Deployment updates live in under 1 minute
- Monitoring with CloudWatch alarms
- Access logging enabled for traffic visibility
- Scalable and low-cost cloud architecture

## Tech Stack
- AWS S3
- AWS CodePipeline
- AWS CloudWatch
- AWS IAM
- GitHub
- GitHub Actions / GitHub Integration
- HTML
- CSS
- Static Hosting
- CI/CD

## Architecture Workflow
GitHub Push → CodePipeline Detects Change → Pulls Latest Code → Deploys Files to S3 → Website Updated Live

## Project Setup
### 1. Website Files Created
- `index.html`
- `404.html`

These files were created as the main portfolio homepage and custom error page.
### 2. S3 Bucket Configuration
#### Created an S3 bucket for static website hosting.
- Bucket Name: `devyansh-portfolio-site`
- Region: `us-east-1`
#### Configured:
- Disabled Block Public Access
- Enabled Static Website Hosting
- Index Document: `index.html`
- Error Document: `404.html`
#### Website Endpoint: `http://devyansh-portfolio-site.s3-website-us-east-1.amazonaws.com`
### 3. Bucket Policy for Public Access
Configured a bucket policy to allow public read access for website files.
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicRead",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::devyansh-portfolio-site/*"
    }
  ]
}
```
### 4. Initial Manual Deployment
#### Uploaded files manually for first validation:
- index.html
- 404.html
#### Verified successful website loading using the S3 website endpoint.
### 5. CI/CD Pipeline Setup
Created an AWS CodePipeline to automate deployments.
#### Pipeline Details
- Pipeline Name: `portfolio-pipeline`
- Source Provider: GitHub
- Repository: `devyansh-ds/portfolio-website`
- Branch: `main`
- Auto Change Detection: Enabled
#### Deploy Stage
- Deploy Provider: Amazon S3
- Bucket: `devyansh-portfolio-site`
- Extract Before Deploy: Enabled
### 6. Automated Deployment Process
Whenever code is pushed to GitHub:
```bash
git add .
git commit -m "Updated homepage"
git push origin main
```
Pipeline automatically runs and deploys latest files.
#### Deployment Flow
- CodePipeline detects new commit
- Pulls source artifact from GitHub
- Extracts files
- Uploads updated files to S3
- Website updates automatically
## Deployment Time
Typical deployment speed:
- Source Stage: 15–30 seconds
- Deploy Stage: 15–30 seconds
- Total Time: 30–60 seconds

## Monitoring & Logging
### CloudWatch Alarm
Configured alerts for pipeline failures.
- Metric: `pipeline-execution-failure`
- Threshold: `>= 1 within 5 minutes`
- Notification: Email via SNS
### S3 Access Logs
Enabled server access logging.
- Log Bucket: `devyansh-portfolio-logs`
Used for tracking website traffic and access requests.

## Skills Demonstrated
- AWS Cloud Fundamentals
- Static Website Hosting
- IAM & Access Control
- CI/CD Automation
- GitHub Integration
- Deployment Pipelines
- Monitoring & Alerts
- Logging & Troubleshooting
- DevOps Basics

## Real-World Impact
- Eliminated manual deployments
- Faster release cycle
- Better consistency between versions
- Improved reliability
- Production-ready hosting workflow

## Future Enhancements
- Add custom domain with Route 53
- Configure HTTPS using CloudFront + ACM
- Build contact form using API Gateway + Lambda + SES
- Add Google Analytics
- Create AWS Budget alerts
- Improve frontend design and responsiveness

## Final Outcome
Successfully built a real cloud project with:
- Live portfolio website hosted on AWS
- Automated CI/CD deployment pipeline
- Monitoring and failure alerts
- Logging enabled
- Hands-on DevOps experience
