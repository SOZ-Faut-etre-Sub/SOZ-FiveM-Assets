![Banniere_SOZ_OSS](https://github.com/SOZ-Faut-etre-Sub/SOZ-FiveM-Server/raw/oss/docs/images/banner-soz-oss.png)

# Assets for FiveM

Splitting assets in a project, such as images and audio, helps in optimizing the loading time and performance.
By separating these assets, the FiveM embedded browser can cache them more effectively, reducing the need to re-download unchanged files and downloading only the necessary assets when needed.
This approach minimizes bandwidth usage and speeds up load times, enhancing the user experience.
Additionally, hosting these assets on a static web server, S3 bucket, or through a CDN like Cloudflare can further improve performance by leveraging distributed networks to deliver content quickly and reliably to users.
This setup also offloads the download from the main server, ensuring better scalability and availability.

## Deployment

There are several ways to publish assets for a project, each with its own benefits.
You can host assets on a static web server, which is straightforward and allows for easy management of files.
Alternatively, using an S3 bucket provides scalable storage with high availability and durability, making it ideal for large-scale applications.
Additionally, leveraging a CDN like Cloudflare can significantly improve performance by distributing content across multiple servers worldwide, reducing latency and ensuring faster load times for users, especially those in geographically distant locations.
Below is an example of how to publish assets using an Nginx server, which involves configuring Nginx to serve your assets from a specified directory, ensuring efficient and reliable delivery of your content.

### Publishing with Nginx

1. **Install Nginx:**

If you haven't already, install Nginx on your server. You can do this using your package manager. For example, on Ubuntu:
```sh
sudo apt update
sudo apt install nginx
```

2. **Configure Nginx:**

Create a new Nginx configuration file for your site. For example, create `/etc/nginx/sites-available/soz-assets` and add the following configuration:
```nginx
server {
  listen 80;
  server_name your-public-endpoint.com;

  location /static/game/ {
      root /path/to/your/public/assets;
      try_files $uri $uri/ =404;
  }
}
```

3. **Enable the Configuration:**

Create a symbolic link to enable the site configuration:
```sh
sudo ln -s /etc/nginx/sites-available/soz-assets /etc/nginx/sites-enabled/
```

4. **Restart Nginx:**

Restart the Nginx service to apply the changes:
```sh
sudo systemctl restart nginx
```
Your public assets should now be accessible via the URL specified in the `server_name` directive in your Nginx configuration.

## Setting Up FiveM Public Assets with `soz_public_endpoint`

To set up the `soz_public_endpoint` variable for a FiveM server, you need to configure it in the `global.cfg` file.
This variable should be set to the URL where your public assets will be hosted. For example, you can set it as follows:

```ini
setr soz_public_endpoint "http://your-public-endpoint.com"
```
