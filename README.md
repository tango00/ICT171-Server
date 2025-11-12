# My Webserver Project
## Triton De Vera | 35723501

This project documents how I set up a webserver on an AWS EC2 instance and deployed a simple website with HTML, CSS and images. 

## Link to Website
www.tritondeveraportfolio.com

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
<img width="1634" height="627" alt="Screenshot 2025-11-11 144943" src="https://github.com/user-attachments/assets/abbf99f8-4550-4333-8f3c-75626ca1b295" />
<img width="814" height="636" alt="Screenshot 2025-11-11 150243" src="https://github.com/user-attachments/assets/54292a36-4317-45cb-8dd6-66a1c061a05c" />

I launched a **t3.micro** EC2 instance on AWS and used the **public IP** to connect via SSH:  

```bash
ssh -i "your-key.pem" ubuntu@<public-ip>
```

This allows remote access to the server so I can install software and configure it.

### 2. Update and Upgrade Packages
<img width="656" height="20" alt="Screenshot 2025-11-11 150323" src="https://github.com/user-attachments/assets/90a7aa2f-0c01-44d3-9da5-3f406a00278c" />

```bash
sudo apt update && sudo apt upgrade -y
```

That line of command updates the package list to make sure you have the latest, available software. It also upgrades all installed packages to their newest versions without asking for confirmation. 

This ensures the server is secure and up to date before installing new softwares. 

### 3. Install Apache2
<img width="626" height="147" alt="Screenshot 2025-11-11 150417" src="https://github.com/user-attachments/assets/69b2ba3a-5273-4ae9-a503-182831df3bf1" />

```bash
sudo apt install apache2 -y
```

Apache2 is a web server software. It handles HTTP requests and serves as HTML, CSS, JS and images to visitors.

### 4. Enable and Start Apache2 Service
<img width="1045" height="96" alt="Screenshot 2025-11-11 150502" src="https://github.com/user-attachments/assets/0e9779bd-a091-450f-b0e2-3f79d6c07134" />

```bash
sudo systemctl enable apache2
sudo systemctl start apache2
```

This makes Apache start automatically every time the server boots and it starts the service immediately so the website can be accessed.

## 5. Configure FireWall
<img width="784" height="287" alt="Screenshot 2025-11-11 150724" src="https://github.com/user-attachments/assets/dbe8a757-bebe-47a5-85c6-1bc9f3bf4964" />

```bash
sudo ufw allow 'Apache Full'
sudo ufw enable
```

The first line opens firewall ports 80 and 443 so web traffic can reach the server. The second line activates the firewall with the new rules. 

### 6. Create Website Directory Structure
<img width="716" height="68" alt="Screenshot 2025-11-11 151303" src="https://github.com/user-attachments/assets/34ebd166-df97-46ae-8d16-011c0fae6c42" />
<img width="911" height="46" alt="Screenshot 2025-11-12 173727" src="https://github.com/user-attachments/assets/c7b66c12-d972-4e52-9a27-99502511e913" />

```bash
sudo mkdir /var/www/html/{css,images,js}
```

This creates folders for CSS, images, and JavaScript, keeping the webstie organized. 

### 7. Create Website Files
<img width="470" height="193" alt="Screenshot 2025-11-12 173746" src="https://github.com/user-attachments/assets/37be87fa-6bab-4158-8e46-8c112edb978f" />

```bash
sudo nano index.html
sudo nano projects.html
sudo nano misc.html
sudo nano blog.html
sudo nano css/style.css
```

The HTML files are the pages for my website. The CSS file controls the design and layout. 

### 8. Upload Files and Images
<img width="1842" height="287" alt="Screenshot 2025-11-12 171655" src="https://github.com/user-attachments/assets/04ab1fe0-c7e9-49d4-b2b6-80c885d4fe87" />
<img width="1845" height="119" alt="Screenshot 2025-11-12 172526" src="https://github.com/user-attachments/assets/5144e5c2-5d2f-46fa-af0a-a9406d511c94" />
<img width="746" height="129" alt="Screenshot 2025-11-12 172613" src="https://github.com/user-attachments/assets/bfc50acb-30ff-47c9-8f89-4f1fd0e9bd0a" />

```bash
scp -i "your-key.pem" localfile ubuntu@<public-ip>:/var/www/html/
sudo cp -r source destination
```

This copies files from my computer to the server so the website is fully functional. 

### 9. Set Permissions and Ownership
<img width="867" height="182" alt="Screenshot 2025-11-12 174538" src="https://github.com/user-attachments/assets/49b28e4e-1094-46bc-a34e-303e28142de9" />

```bash
sudo chown -R www-data:www-data /var/www/html
sudo chmod 755 -R /var/www/html
```

The first line changes owner and group of all files to www-data allowing the server to access the files.
The second line gives the owner full access, and everyone else read/execute permissions. This ensures the website is secure but is still accessible to the public. 

### 10. Restart Apache2
<img width="593" height="25" alt="Screenshot 2025-11-12 174734" src="https://github.com/user-attachments/assets/897a9af4-c41a-4ffc-9ba4-15bf3eb9cf3b" />

```bash
sudo systemctl restart apache2
```

Restarting Apache is done to apply any changes to files, directories, or permissions so the server runs smoothly. 

### 11. Enable HTTPS with Let’s Encrypt

```bash
sudo apt update 
sudo apt install certbot python3-certbot-apache
sudo certbot --apache
```

Certbot will automatically configure Apache and issue a free SSL certificate. This allows the server to use https. 

### 12. Set Up DNS
<img width="1901" height="957" alt="Screenshot 2025-11-12 182842" src="https://github.com/user-attachments/assets/48667a34-7ab5-473c-b6de-cfce47a396a3" />
<img width="1919" height="956" alt="Screenshot 2025-11-12 183204" src="https://github.com/user-attachments/assets/3f3de623-654d-49e3-95bb-399134c3eaa6" />
<img width="1308" height="360" alt="Screenshot 2025-11-12 183750" src="https://github.com/user-attachments/assets/5cdd3356-a498-435f-8a4b-c6183ce8f21b" />

I purchased a domain on GoDaddy and linked it to my EC2 Instance's IP address to make my website accessible via a custom domain. Then I connected my IP to the domain name. 

--- 
That is how I made this web server. As I said in the Project Proposal, I used AI to help me out with issues and with learning how to code in HTML. However, the idea and the creation is by me. I bumped into a lot of technical difficulties and a lot of errors; without the use of AI to summarize the errors and help me learn, I wouldn't be able to have completed this project. 












