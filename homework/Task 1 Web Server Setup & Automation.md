

## Web Server Setup & Automation

**Objective**: Set up a Nginx web server with automated deployment of a static website.  

Tasks:


- Install Nginx and ensure it starts on boot.
```
sudo apt install nginx
```

- Create a directory /var/www/lab-site and add a sample index.html with the text "Welcome to Intern Lab"
```
cd /var/www/
```

```
mkdir index.html
```

```
touch index.html
```




-  Configure Nginx to Serve the Site on Port 8080

Now, configure Nginx to serve the site from `/var/www/lab-site` on port 8080. Create a new configuration file for your site.

```
sudo nano /etc/nginx/sites-available/lab-site

```

Add the following configuration to the file:
```
server {
    listen 8080;
    server_name localhost;

    root /var/www/lab-site;
    index index.html;


}
```

creating a soft link 
sudo ln -s /etc/nginx/sites-available/lab-site /etc/nginx/sites-enabled/
