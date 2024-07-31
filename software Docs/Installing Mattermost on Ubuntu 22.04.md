# Installing Mattermost on Ubuntu 22.04



## Introduction 

Mattermost is an open-source, self-hosted team communication platform that offers a secure and flexible alternative to Slack and other messaging platforms. This guide provides a step-by-step process for installing Mattermost on Ubuntu 22.04, including prerequisites, installation, configuration, and troubleshooting.



## Glossary

- **Mattermost**: An open-source team communication tool.
- **Ubuntu**: A popular Linux distribution based on Debian.
- **Nginx**: A high-performance web server and reverse proxy.
- **PostgreSQL**: An open-source relational database management system.
- **Systemctl**: A command-line utility to manage systemd services.
- **DNS**: Domain Name System, which translates domain names to IP addresses.



## Prerequisites 

Before installing Mattermost, ensure the following are in place:

1. **Ubuntu 22.04 Server**: A fresh installation of Ubuntu 22.04.
2. **Root Access**: You need to have sudo privileges.
3. **Domain Name**: (Optional) A registered domain name, properly configured with DNS settings.



## In this article

1. Instalation Steps

   1.1 Update the system.

   1.2 Install Dependencies.

   1.3 Install PostgreSQL.

   1.4 Download and Install Mattermost.

   1.5 Configure Mattermost.

   1.6 Set up Systemd Service.

   1.7 Install and configure Nginx

---



## Installation Steps

### 1. Update the System

Start by updating the package lists and upgrading the installed packages:

```bash
sudo apt update
sudo apt upgrade -y
```

### 2. Install Dependencies

Install the necessary software packages:

```bash
sudo apt install -y curl wget gnupg2 lsb-release
```

### 3. Install PostgreSQL

Mattermost uses PostgreSQL as its database. Install PostgreSQL and set up the database:

```bash
sudo apt install -y postgresql postgresql-contrib
```

Create the Mattermost database and user:

```bash
sudo -u postgres psql
```

Within the PostgreSQL prompt:

```sql
CREATE DATABASE mattermost;
CREATE USER mattermost WITH PASSWORD 'your_password';
GRANT ALL PRIVILEGES ON DATABASE mattermost TO mattermost;
\q
```

### 4. Download and Install Mattermost

Download the latest Mattermost release:

```bash
wget https://releases.mattermost.com/5.37.3/mattermost-5.37.3-linux-amd64.tar.gz
```

Extract the downloaded file and move it to the appropriate directory:

```bash
tar -xvzf mattermost-5.37.3-linux-amd64.tar.gz
sudo mv mattermost /opt/
```

Create the data directory:

```bash
sudo mkdir /opt/mattermost/data
```

Create an user for Mattermost and give permissions:

```bash
sudo useradd --system --user-group mattermost
sudo chown -R mattermost:mattermost /opt/mattermost
sudo chmod -R g+w /opt/mattermost
```

Create a symlink to the Mattermost binary:

```bash
sudo ln -s /opt/mattermost/bin/mattermost /usr/local/bin/mattermost
```

### 5. Configure Mattermost

Edit the Mattermost configuration file:

```bash
sudo nano /opt/mattermost/config/config.json
```

Update the `SqlSettings` section to match your PostgreSQL setup:

```
"SqlSettings": {
    "DriverName": "postgres",
    "DataSource": "postgres://mattermost:your_password@localhost:5432/mattermost?sslmode=disable",
    ...
}
```

![GNU nano](pics/pic2.png)

You can press `ctrl + 0` to save changes, then press `enter` to confirm you want to save the current file and finally press `ctrl + x` to exit the `nano`editor. 

### 6. Set Up Systemd Service

Create a systemd service file for Mattermost:

```bash
sudo nano /etc/systemd/system/mattermost.service
```

Add the following content:

```ini
[Unit]
Description=Mattermost
After=network.target

[Service]
Type=simple
User=mattermost
Group=mattermost
ExecStart=/opt/mattermost/bin/mattermost
Restart=always
LimitNOFILE=49152

[Install]
WantedBy=multi-user.target
```

Reload systemd and start the Mattermost service:

```bash
sudo systemctl daemon-reload
sudo systemctl start mattermost
sudo systemctl enable mattermost
```

Start and enable the Mattermost service:

```bash
sudo systemctl start mattermost
sudo systemctl enable mattermost
```



### 7. Install and Configure Nginx

Install Nginx:

```bash
sudo apt install -y nginx
```

Create an Nginx configuration file for Mattermost:

```bash
sudo nano /etc/nginx/sites-available/mattermost
```

Add the following content:

```nginx
server {
    listen 80;
    server_name your_domain_or_IP;

    location / {
        proxy_pass http://localhost:8065;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Remember to modify `your_domain_or_IP` with your actual domain.

Enable the new site and restart Nginx:

```bash
sudo ln -s /etc/nginx/sites-available/mattermost /etc/nginx/sites-enabled/
sudo systemctl restart nginx
```

You can also check the nginx status to verify if its active:

```bash
sudo systemctl status nginx
```

![nginx](pics/pic3.png)



Now, you can access to Mattermost.

![Mattermost](pics/pic1.png)





