# My Webserver Project
## Triton De Vera | 35723501

This project documents how I set up a webserver on an AWS EC2 instance and deployed a simple website with HTML, CSS and images. 

## Link to Website


## Link to Video Explainer

## Requirements

- AWS account  
- EC2 instance (I used **t3.micro**)  
- SSH access to EC2  
- Apache2 web server  
- HTML/CSS/JS files for the website  
- GoDaddy domain for DNS  

---

## Setup Instructions

### 1. Launch EC2 Instance and Connect via SSH

I launched a **t3.micro** EC2 instance on AWS and used the **public IP** to connect via SSH:  

```bash
ssh -i "your-key.pem" ubuntu@<public-ip>
```

This allows remote access to the server so I can install software and configure it.

### 2. Update and Upgrade Packages

```bash
sudo apt update && sudo apt upgrade -y
```

That line of command updates the package list to make sure you have the latest, available software. It also upgrades all installed packages to their newest versions without asking for confirmation. 

This ensures the server is secure and up to date before installing new softwares. 

### 3. Install Apache2

```bash
sudo apt install apache2 -y
```

Apache2 is a web server software. It handles HTTP requests and serves as HTML, CSS, JS and images to visitors.

### 4. Enable and Start Apache2 Service

```bash
sudo systemctl enable apache2
sudo systemctl start apache2
```

This makes Apache start automatically every time the server boots and it starts the service immediately so the website can be accessed.

## 5. Configure FireWall

```bash
sudo ufw allow 'Apache Full'
sudo ufw enable
```

The first line opens firewall ports 80 and 443 so web traffic can reach the server. The second line activates the firewall with the new rules. 

### 6. Create Website Directory Structure

```bash
sudo mkdir /var/www/html/{css,images,js}
```

This creates folders for CSS, images, and JavaScript, keeping the webstie organized. 

### 7. Create Website Files

```bash
sudo nano index.html
sudo nano projects.html
sudo nano misc.html
sudo nano blog.html
sudo nano css/style.css
```

The HTML files are the pages for my website. The CSS file controls the design and layout. 

### 8. Upload Files and Images

```bash
scp -i "your-key.pem" localfile ubuntu@<public-ip>:/var/www/html/
sudo cp -r source destination
```

This copies files from my computer to the server so the website is fully functional. 

### 9. Set Permissions and Ownership

```bash
sudo chown -R www-data:www-data /var/www/html
sudo chmod 755 -R /var/www/html
```

The first line changes owner and group of all files to www-data allowing the server to access the files.
The second line gives the owner full access, and everyone else read/execute permissions. This ensures the website is secure but is still accessible to the public. 

### 10. Restart Apache2

```bash
sudo systemctl restart apache2
```

Restarting Apache is done to apply any changes to files, directories, or permissions so the server runs smoothly. 

### 11. Set Up DNS

I purchased a domain on GoDaddy and linked it to my EC2 Instance's IP address to make my website accessible via a custom domain. 

--- 
That is how I made this web server. As I said in the Project Proposal, I used AI to help me out with issues and with learning how to code in HTML. However, the idea and the creation is by me. 












