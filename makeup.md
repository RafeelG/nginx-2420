# Make-up Assignment Instructions

## Step 1: install Necessary Software
```bash
sudo pacman -Syu
sudo pacman -S nginx
```
### This is to update your packages and install nginx as well as vim

## Step 2: Create Directories
```bash 
sudo mkdir -p /etc/nginx/sites-available
sudo mkdir -p /etc/nginx/sites-enabled
sudo mkdir -p /srv/2420-files
```
### This creates the directories you need. Sites available direcotry will contain Nginx server block configurations. The sites-enabled directory will contain symbolic links to the configurations you want to enable. The /srv/2420-files directory will contain the files you want to serve.

## Step 3: Add Server Block to Sites-Available
```bash
sudo vim /etc/nginx/sites-available/file_server
```
### Add this inside the file don't forget to replace your_IP with your actual IP
```bash
server {
    listen 80;
    server_name your_IP;
    location / {
        root /srv/2420-files;
        autoindex on;
    }
}

### This configuration tells Nginx to listen on port 80 for requests to your domain or IP address. When it receives a request, it serves files from the /srv/2420-files directory
```
## Step 4: Enable the Server Block
```bash
sudo ln -s /etc/nginx/sites-available/file_server /etc/nginx/sites-enabled/
```

## Step 5: Test the Nginx Configuration
```bash 
sudo nginx -t 
```
### This checks the Nginx configuration for syntax errors.

## Step 6: Restart Nginx
```bash
sudo systemctl restart nginx
```

## Step 7: Add files to your 2420-files folder:
### go into the folder:
```bash
cd /srv/2420-files
```
### add a file
```bash
sudo touch my_file.txt
```

## Step 8: Test your server 
### To test your server your ip address into the browser; you should see a list of files in the /srv/2420-files directory

