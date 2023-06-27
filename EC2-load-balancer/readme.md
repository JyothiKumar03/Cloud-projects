# **LOAD BALANCER DEMO**
## *A demonstration of Load-Balancer in Cloud Infrastructure using AWS and nginx server*

### Tech Stack used - AWS EC2 service, nginx server

*Workflow* - Creating 2 EC2 Instances and setting up a Load-Balancer Between them for equal distribution of requests.

**Amazon Web Services are one of the major cloud service provider in the market. Elastic Compute Cloud (EC2) is a compute engine offered by AWS**
> *EC2* - A compute service provided by Amazon services where we can run instances, create virtual machines and use them for computing services

## *Features of EC2  *

+  **Scalability** - scaling application according to our requirment
+  **Flexibility** - Choose from a wide range of instance types optimized for various use cases, including general-purpose, memory-optimized, GPU instances, and more.
+  **High Avalibility** - AWS provides options for availability zones and regions, allowing you to distribute your instances across multiple data centers
+  **Security** - virtual private clouds (VPCs), security groups, key pairs, and IAM (Identity and Access Management) roles, ensuring the security of your instances and data.
+ **Elastic IP** - Assign static IP addresses to your instances to make them easily accessible even if they are stopped or restarted.
+ **Amazon Machine Images (AMIs)** - Pre-configured templates that include operating systems and software configurations, allowing you to quickly launch instances with the desired setup.

## *Step-1 Creating EC2 Instances*

## Steps to Create an EC2 Instance (General Steps)**
1. Sign up for an AWS account if you don't have one already.
2. Open the AWS Management Console and navigate to the EC2 service.
3. Create a key pair that will be used to securely connect to your instances.
4. Launch an EC2 instance by selecting an Amazon Machine Image (AMI) and an instance type.(Amazon ubuntu for Free tier)
5. Configure the instance settings, including security groups, network, storage, and tags.
6. Review and launch the instance.
7. Connect to your instance using SSH or other remote access methods.
8. Install the necessary software and configure your applications on the instance.

*For our Load-balancing application, we need 2 instances so that the overload of requests can be directed from one instance to other*
![Screenshot (10)](https://github.com/JyothiKumar03/Cloud-projects/assets/88045362/11edb04b-65df-4b5d-9cac-ddee50744671)

As mentioned, 2 instances are created under the same network!!
Now, we need to establish a load-balancer for directing the request-load. Nginx is used to do that!!

![image](https://github.com/JyothiKumar03/Cloud-projects/assets/88045362/60f55412-d40c-4805-b8df-65eed4039bff)
## *Nginx - High Performance Web Server* 
 Its a high-performance web server and reverse proxy server. Nginx is widely used for serving static and dynamic content, as well as for load balancing, caching, and improving the overall performance of web applications.

## Features 
+  ***High Performance***: Nginx is designed to handle a large number of concurrent connections and deliver content quickly, making it suitable for high-traffic websites and applications.
+  ***Reverse Proxy***: Nginx acts as a reverse proxy server, enabling you to distribute incoming requests across multiple backend servers for load balancing and improved performance.
+  ***HTTP Server***: It serves as a powerful HTTP server capable of handling various HTTP/HTTPS requests, including static file serving, virtual hosting, SSL/TLS termination, and more.
+  ***Caching***: Nginx can cache frequently accessed content, reducing the load on backend servers and improving response times for subsequent requests.
+  ***Flexible Configuration***: Nginx uses a declarative configuration syntax that allows you to customize and fine-tune its behavior according to your specific requirements.
+  ***SSL/TLS Support***: Nginx supports SSL/TLS encryption, allowing you to secure your connections and protect sensitive data transmitted over the network.
+  ***Dynamic Module System***: Nginx's modular architecture allows you to extend its functionality by adding various third-party and custom modules.
  
![image](https://github.com/JyothiKumar03/Cloud-projects/assets/88045362/d3f82f14-9947-46a0-9a1b-ec17406be545)

## *Steps to setup nginx server*
1. Download and install Nginx on your server or machine. Nginx provides official packages for various operating systems, or you can compile it from source.
2. Configure Nginx by editing the main configuration file (nginx.conf). This file specifies the behavior of the server, including server blocks, HTTP settings, and more.
3. Start the Nginx service. The process may vary depending on your operating system, but typically, you can use commands like systemctl start nginx or service nginx start.
4. Verify that Nginx is running by accessing your server's IP address or domain name in a web browser. If configured correctly, you should see the default Nginx welcome page.

**Configuration** - Nginx has a configuration file which describes the load-balancing architecture. We have to create it
+  ***Server Blocks***: Define virtual hosts to handle different domains or subdomains. Each server block specifies the root directory, access rules, SSL/TLS settings, and more for a specific site.
+  ***HTTP Settings***: Configure general HTTP settings such as timeouts, buffer sizes, gzip compression, MIME types, and more.
+  ***Location Blocks***: Customize the behavior for specific URL patterns or directories, including proxying requests, enabling caching, or applying access restrictions.
+  ***Upstreams***: Define groups of backend servers for load balancing or proxying purposes.

 ## Nginx Configuration

The following is an example of a basic Nginx configuration:

```nginx
# Set the number of worker processes based on the number of CPU cores
worker_processes auto;

# Define the events block to optimize connections handling
events {
  worker_connections 1024;
}

http {
  # Set the MIME types to handle different file extensions
  include mime.types;

  # Default file types to serve
  default_type application/octet-stream;

  # Configure logging
  access_log /var/log/nginx/access.log;
  error_log /var/log/nginx/error.log;

  # Configure the server
  server {
    # Listen on port 80 for HTTP requests
    listen 80;

    # Server name (replace example.com with your domain)
    server_name example.com;

    # Root directory for the website files
    root /var/www/html;

    # Enable gzip compression for faster content delivery
    gzip on;
    gzip_types text/plain text/css application/javascript image/*;

    # Handle requests for static files
    location / {
      # Enable directory indexing if no index file is found
      index index.html;

      # Try to serve the requested file
      try_files $uri $uri/ =404;
    }
  }
}
```

In this example, the Nginx configuration sets the number of worker processes and connections for optimal performance. It includes the MIME types, logging locations, and a server block that listens on port 80 for HTTP requests.

The server block specifies the server name (replace `example.com` with your actual domain) and the root directory for the website files. It also enables gzip compression for faster content delivery and defines the behavior for handling requests for static files using the location block.

Remember to adjust the configuration according to your specific setup, including the server name, root directory, and any other relevant settings.
