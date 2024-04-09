# instructions 2

## Step 1: Setup your server 
'''bash
sudo pacman -Syu
sudo pacman -S nginx git ufw 
'''

## Step 2: Place backend binary on your system 
### First, you need to transfer the hello-server binary to your server. You've already done this using the sftp command:
'''bash
sftp -i /Users/rafee/.ssh/do-key arch@64.23.139.205
put hello-server
exit
'''

### Once the binary is on your server, move it to the appropriate directory and make it executable:
'''bash
sudo mv your_backend_binary /usr/local/bin/
sudo chmod +x /usr/local/bin/your_backend_binary
'''

## Step 3: Create a New Service File for the Backend
### Create a new systemd service file for your backend. This will allow it to run as a service:
'''bash
sudo nano /etc/systemd/system/backend.service
'''
### Add this following content to the file:
'''bash
[Unit]
Description=Backend Service
After=network.target

[Service]
ExecStart=/usr/local/bin/hello-server
Restart=always

[Install]
WantedBy=multi-user.target
'''
### Enable the service 
'''bash 
sudo systemctl enable backend
sudo systemctl start backend
'''
## Step 4: Reverse Proxy 
'''bash
sudo vim /etc/nginx/sites-available/backend
'''
### Add the configuration into this, don't forget to replace your_domain_or_IP with your actually IP
'''bash
server {
    listen 80;
    server_name your_domain_or_IP;
location /hey {
        proxy_pass http://127.0.0.1:8080/;
    }

    location /echo {
        proxy_pass http://127.0.0.1:8080/;
    }
  }
'''
### Enable the site by creating a symbolic link to the sites-enabled directory:
'''bash 
sudo ln -s /etc/nginx/sites-available/backend /etc/nginx/sites-enabled/
'''
### Test the Nginx configuration and reload Nginx:
'''bash
sudo nginx -t
sudo systemctl restart nginx
'''
## Step 5: Configure UFW Firewall
### allow http and https through the firewall
'''bash
sudo ufw allow http
sudo ufw allow https
'''
### Enable UFW:
'''bash
sudo ufw enable
'''
## Step 6: Test your Backend
### Test your backend using curl or postman; don't forget to replace your_domain_or_IP with your server's domain or IP address:
'''bash
curl http://your_domain_or_IP/hey
curl -X POST -H "Content-Type: application/json" -d '{"message": "Hello from your server"}' http://your_domain_or_IP/echo
'''




