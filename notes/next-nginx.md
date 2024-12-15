## Deploying a Next.js Application with Docker and Nginx on Ubuntu (VPS Hosting)

### Step 1: Update and Upgrade System Packages

```bash
sudo apt update && sudo apt upgrade -y
```

### Step 2: Set up Docker's apt repository.

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

> **Note**
> If you use an Ubuntu derivative distribution, such as Linux Mint, you may need to use `UBUNTU_CODENAME` instead of `VERSION_CODENAME`

### Step 3: Install the Docker packages.

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Step 4: Verify that the installation is successful by running the hello-world image.

```bash
sudo sudo docker run hello-world
docker --version
docker-compose --version

```

### Step 5: Clone Your Next.js Application Repository.

```bash
# Navigate to the directory where you want to clone the repository
cd /var/www

# Clone the repository from GitHub (replace <repository-url> with your repo URL)
git clone <repository-url> my-nextjs-app

# Navigate to the project directory
cd my-nextjs-app

```

### Step 6: Set Up Your .env File

```bash
# Create the .env file and add your environment variables
nano .env

# Example of .env contents:
# NODE_ENV=production
# DATABASE_URL=your_database_url
# PORT=3000

```

### Step 7: Build and Start Your Application make sure you have dockerfile and docker compose to your repository

```bash
# Build and start the application using Docker Compose detached mode
docker-compose up --build -d
```

### Step 8: Configure Firewall

```bash
# If you have enabled UFW firewall, you need to add ports HTTP and HTTPS:
ufw allow 80/tcp
ufw allow 443/tcp
ufw reload
```

### Step 9: Configure Firewall

```bash
# If you have enabled UFW firewall, you need to add ports HTTP and HTTPS:
ufw allow 80/tcp
ufw allow 443/tcp
ufw reload
```

### Step 10: Install and Configure Nginx as a Reverse Proxy

```bash
# Install Nginx:
sudo apt install nginx -y
```

```bash
# Create a new Nginx configuration file for your application:
sudo nano /etc/nginx/sites-available/your-nextjs-app
```

```bash
# Add the following configuration:
server {
    server_name your_domain;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }

    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/your_domain/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/your_domain/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

}
server {
    if ($host = your_domain) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


    listen 80;
    server_name your_domain;
    return 404; # managed by Certbot
}
```

Replace your_domain_or_ip with your domain name or server IP address. Save and close the file.

Create a symbolic link to enable this configuration:

```bash

# Enable the Nginx configuration
sudo ln -s /etc/nginx/sites-available/nextjs /etc/nginx/sites-enabled/

# Test and restart Nginx
sudo nginx -t
sudo systemctl restart nginx

```

### Step 11: Secure Your Application with Let's Encrypt

```bash

# Install Certbot
sudo apt install certbot python3-certbot-nginx -y

# Obtain and configure SSL certificates
sudo certbot --nginx -d your_domain

# Test auto-renewal
sudo certbot renew --dry-run


```

### Step 12: Verify Your Deployment

Your Next.js application should now be running on your domain `https://your_domain`. Visit your domain in a web browser to verify that everything is working correctly.
