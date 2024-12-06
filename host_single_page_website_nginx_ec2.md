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
echo '<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html>
<head>
<style text="text/css">
body {background-color:#e4e2e0;}
h3 {color:#e52c1a;font-style:italic;
    padding:5px;
	border-color:#673622;
    border-style:dashed;}
h1 {color:#673622;
    background-color:white;}
h2 {color:#673622;
    background-color:yellow;}
p{font-family:arial;}
p,h1,h2,h3,h4,a,table{font-family:arial;}
a:link{color:black}
a:visited{color:blue}
a:hover{background-color:blue;
color:white;
text-decoration:none;
font-style:bold;}
a:active{background-color:orange;}
table{border:3px solid black;
      background-color:yellow;}
tr{background-color:white;}

	   
</style>
</head>
<body>
<h1>IELTS</h1>
<p><a href = "IELTS_HOME.html" title="Homepage"><img src="home.png"/></a></p>
<h2>(International English Language Testing System)</h2>
<p>

IELTS is the International English Language Testing System. It is the world's most popular English language test for higher education and global migration, with over 2 million IELTS tests taken in the last year. The British Council offers IELTS tests and preparation courses in our centres throughout the world.

</p>
<table border="1">
<tr colspan="3">
<td><strong><a href= "IELTS_WRITING.html" title="Writing introduction">WRITING </a></strong></td>
<td><strong>SPEAKING</strong></td>
<td><strong>LISTNING</strong></td>
<td><strong>READING</strong></td>
</tr>
<tr>
<td><strong><a href= "IELTS_WRITING1.html" title="Writing task 1 examples">Writing Task 1</a></strong></</td>
<td><strong><a href="IELTS_SPEAKING2.html" title="Speaking part 1 examples">Speaking Part 1</a></strong></td>
<td><strong>LISTNING</strong></td>
<td><strong>READING</strong></td>
</tr>
<tr>
<td><strong><a href= "IELTS_WRITING2.html" title="Writing task 2 examples">Writing Task 2</a></strong></td>
<td><strong><a href="IELTS_SPEAKING1.html"title="Speaking part 2 examples">Speaking Part 2</a></strong></td>
<td><strong>LISTNING</strong></td>
<td><strong>READING</strong></td>
</tr>

</table>

</body>
</html>' > index.html
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


    location / {
        root   /usr/share/nginx/html;
        index  index.html;
        try_files $uri $uri/ /index.html;
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
