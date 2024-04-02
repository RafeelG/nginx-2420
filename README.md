# nginx-2420
# Setting up a new server with Nginx on Arch Linux

This tutorial will guide you through the process of setting up a new server with Nginx on Arch Linux.

## Prerequisites

- A fresh Arch Linux server
- Root or sudo access

## Step 1: Update the system

First, make sure your system is up-to-date:

```bash
sudo pacman -Syu

## Step 2: Install necessary software

Next, install Vim and Nginx:
sudo pacman -S vim nginx

## Step 3: Create Nginx Configuration Directories

Create the sites-available and sites-enabled directories:
sudo mkdir -p /etc/nginx/sites-available
sudo mkdir -p /etc/nginx/sites-enabled

Edit the main Nginx configuration file to include the sites-enabled directory. Open /etc/nginx/nginx.conf:

Add the following line at the end of the http block:
include /etc/nginx/sites-enabled/*;
Save and close the file.





## Step 4: Create the project root directory
Create a new directory /web/html/nginx-2420 that will act as your project root:
sudo mkdir -p /web/html/nginx-2420

## Step 5: Configure Nginx
Create a new server block configuration file for your server:
sudo vim /etc/nginx/sites-available/nginx-2420

In this file, add the following configuration:

server {
    listen 80;
    server_name your_server_ip;

    location / {
        root /web/html/nginx-2420;
        index index.html;
    }
}

Replace your_server_ip with your server's IP address.

## Step 6: Enable the new configuration
To enable the new configuration, create a symbolic link to it in the sites-enabled directory:

sudo ln -s /etc/nginx/sites-available/nginx-2420 /etc/nginx/sites-enabled/

Then, test the configuration:
sudo nginx -t

If the configuration is correct, restart Nginx:
sudo systemctl restart nginx

## Step 7: Create the demo document
Create a new file sudo vim /web/html/nginx-2420/index.html and add the following content:



<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2420</title>
    <style>
        * {
            color: #db4b4b;
            background: #16161e;
        }
        body {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
        }
        h1 {
            text-align: center;
            font-family: sans-serif;
        }
    </style>
</head>
<body>
    <h1>All your base are belong to us</h1>
</body>
</html>

Now, you should be able to access the demo document by navigating to your server's IP address in a web browser.

```![rafeel](https://github.com/RafeelG/nginx-2420/assets/148383119/1d541ea8-cd50-45f6-a6e1-db656bc20bbc)
![rafeel](https://github.com/RafeelG/nginx-2420/assets/148383119/fba356f9-2f8a-41bb-84bc-8f32e60b1f3c)
