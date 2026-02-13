# Lab M2 – HTTP Access with Nginx Reverse Proxy

## Overview
This lab demonstrates how to expose a Node.js application publicly using Nginx as a reverse proxy.

## Steps Followed
1. Allowed HTTP (port 80) in EC2 security group
2. Installed and started Nginx
3. Created a Node.js Express app on port 8080
4. Configured Nginx to proxy requests to the app
5. Tested access locally and via public IP

## Public Access
- Public IP: http://54.224.183.50

## Security Group
- Security Group ID: sg-04cf39bfa425aa786
- Inbound rule: HTTP 80 from 0.0.0.0/0

## Troubleshooting
- Ensured Nginx config passed `nginx -t`
- Verified Node app was listening on port 8080

## Reflection
Using Nginx as a reverse proxy allows applications to run on internal ports while exposing a standard HTTP interface. This improves security, flexibility, and scalability.

