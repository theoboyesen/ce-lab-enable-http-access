# Lab M2.04 - Enable HTTP Access and Configure Web Server

**Repository:** [https://github.com/cloud-engineering-bootcamp/ce-lab-enable-http-access](https://github.com/cloud-engineering-bootcamp/ce-lab-enable-http-access)

**Activity Type:** Individual  
**Estimated Time:** 30-45 minutes

## Learning Objectives

- [ ] Configure security groups to allow HTTP traffic
- [ ] Set up Nginx as a reverse proxy
- [ ] Test traffic flow from internet to application
- [ ] Implement HTTP to HTTPS redirection
- [ ] Verify proper configuration

## Your Task

Configure your EC2 instance to serve a web application publicly:
1. Allow HTTP traffic through security group
2. Install and configure Nginx
3. Deploy a simple Node.js application
4. Configure Nginx to proxy requests
5. Test from internet

**Success:** Public URL serving your application

## Quick Start

```bash
# 1. Update security group - add HTTP (80) from 0.0.0.0/0

# 2. Install Nginx
sudo yum install -y nginx

# 3. Create simple app
mkdir ~/app && cd ~/app
npm init -y
npm install express

cat > index.js <<'EOF'
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send(`
    <h1>Hello from ${process.env.HOSTNAME}!</h1>
    <p>You've successfully configured HTTP access</p>
  `);
});

app.listen(8080, () => {
  console.log('App running on port 8080');
});
EOF

node index.js &

# 4. Configure Nginx proxy
sudo tee /etc/nginx/conf.d/app.conf <<EOF
server {
    listen 80;
    location / {
        proxy_pass http://localhost:8080;
    }
}
EOF

sudo systemctl start nginx

# 5. Test
curl http://$(curl -s ifconfig.me)
```

## 📤 What to Submit

**Submission Type:** File Upload (ZIP)

Create a ZIP file named `lab-m2-http-access.zip` containing:

1. **Nginx Configuration Files:**
   - `/etc/nginx/conf.d/app.conf` (your proxy configuration)
   - `/etc/nginx/nginx.conf` (if modified)

2. **Application Files:**
   - `index.js` (your Node.js application)
   - `package.json`


**File Structure:**
```
lab-m2-http-access.zip
├── README.md
├── configs/
│   ├── app.conf
│   └── nginx.conf (if modified)
├── application/
│   ├── index.js
│   └── package.json
└── screenshots/
    ├── 01-security-group-http-rule.png
    ├── 02-browser-working-webpage.png
    ├── 03-services-running.png
    └── 04-curl-test.png
```

## Grading: 100 points
- Security group configuration: 25pts
- Nginx reverse proxy setup: 25pts
- Application working publicly: 30pts
- Documentation quality: 20pts
