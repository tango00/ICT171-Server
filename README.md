# My Webserver Project

This project documents how I set up a webserver on an AWS EC2 instance and deployed a simple website with HTML, CSS, JavaScript, and images.  

---

## Project Overview

The goal of this project was to launch a webserver on AWS, host a personal website, and link it to a custom domain purchased on GoDaddy.

---

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
