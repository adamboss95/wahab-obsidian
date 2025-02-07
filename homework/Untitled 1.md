






-  Configure Nginx to Serve the Site on Port 8080

Now, configure Nginx to serve the site from `/var/www/lab-site` on port 8080. Create a new configuration file for your site.

```
sudo nano /etc/nginx/sites-available/lab-site

```

Add the following configuration to the file:

server {
    listen 8080;
    server_name localhost;

    root /var/www/lab-site;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}

