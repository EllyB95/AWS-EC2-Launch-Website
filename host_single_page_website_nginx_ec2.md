### 1. Connect to Your EC2 Instance:

```bash
ssh -i path/to/your/key.pem ec2-user@your-ec2-instance-ip
```

### 2. Update Your System:

```bash
sudo yum update -y
```

### 3. Install Nginx:

```bash
sudo yum install nginx -y
```

### 4. Start Nginx:

```bash
sudo systemctl start nginx
```

### 5. Enable Nginx to Start on Boot:

```bash
sudo systemctl enable nginx
```

### 6. Create a Dummy `index.html`:

Create a file named `index.html` with the following content:

```bash
echo '<!DOCTYPE html><html lang="en"><head><meta charset="UTF-8"><meta name="viewport" content="width=device-width, initial-scale=1.0"><title>My Dummy SPA</title></head><body><div id="app"><h1>Welcome to My Dummy SPA</h1><p>This is a dummy single-page application for testing.</p></div></body></html>' > index.html
```

### 7. Copy `index.html` to Nginx's Default Directory:

```bash
sudo cp index.html /usr/share/nginx/html
```

### 8. Configure Nginx:

Edit the Nginx configuration file:

```bash
sudo nano /etc/nginx/nginx.conf
```

Inside the `server` block, update the `location /` block to point to your SPA's build directory:

```nginx
server {
    listen       80;
    server_name  localhost;

    location / {
        root   /usr/share/nginx/html;
        index  index.html;
        try_files $uri $uri/ /index.html;
    }
}
```

### 9. Restart Nginx:

```bash
sudo systemctl restart nginx
```

### 10. Allow HTTP Traffic in Security Group:

- Go to the AWS Management Console.
- Navigate to the EC2 dashboard.
- In the left navigation pane, choose "Security Groups."
- Select the security group associated with your EC2 instance.
- Edit the inbound rules to allow traffic on port 80 (HTTP).

### 11. Access Your SPA:

Open a web browser and enter the public IP address or DNS name of your EC2 instance. You should now see the content of your dummy SPA hosted using Nginx.

That's it! You've successfully set up Nginx to host a simple dummy SPA on an EC2 instance. Adjust the configuration and dummy `index.html` content based on your actual single-page application.
