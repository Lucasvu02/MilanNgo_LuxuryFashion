Milan NGO E-Commerce Website

Project Overview

Milan NGO’s e-commerce website is designed to sell products and merchandise online to support the organization’s charitable missions. The platform offers a smooth shopping experience with secure user registration, product browsing, shopping cart, payment processing, and order tracking. It also includes an admin dashboard for managing products and orders, and showcases the NGO’s story to engage visitors.

Key Features:

Product catalog with categories
User authentication
Cart and checkout
Payment gateway integration
Order management
Responsive design
Tech Stack:

Backend: Django
Database: PostgreSQL
Web server: Gunicorn + Nginx
Frontend: HTML/CSS/JavaScript
Hosting: Ubuntu VPS
Quick Deployment Guide on Ubuntu VPS

Update and install packages:
sudo apt update -y && sudo apt upgrade -y
sudo apt install python3-pip python3-dev libpq-dev postgresql postgresql-contrib nginx curl file
Setup PostgreSQL database and user:
sudo -u postgres psql
CREATE DATABASE milan_ngo;
CREATE USER milanuser WITH PASSWORD 'securepassword';
ALTER ROLE milanuser SET client_encoding TO 'utf8';
ALTER ROLE milanuser SET default_transaction_isolation TO 'read committed';
ALTER ROLE milanuser SET timezone TO 'UTC';
GRANT ALL PRIVILEGES ON DATABASE milan_ngo TO milanuser;
\q
Create Python virtual environment and install dependencies:
sudo -H pip3 install --upgrade pip virtualenv
mkdir ~/milan_project && cd ~/milan_project
virtualenv milanenv
source milanenv/bin/activate
pip install django gunicorn psycopg2-binary pillow
Clone the project and run migrations:
git clone <project_repo_url> .
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
python manage.py collectstatic
Configure Gunicorn with systemd:
Create /etc/systemd/system/gunicorn.service with proper settings to run Gunicorn as a daemon.
Configure Nginx:
Create an Nginx site config to proxy requests to Gunicorn and serve static files.
Enable firewall and start services:
sudo ufw allow 'Nginx Full'
sudo systemctl start gunicorn
sudo systemctl enable gunicorn
sudo systemctl restart nginx
(Optional) Setup SSL with Certbot:
sudo snap install core; sudo snap refresh core
sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot
sudo certbot --nginx
